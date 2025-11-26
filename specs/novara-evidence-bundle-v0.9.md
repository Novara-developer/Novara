# Novara Evidence Bundle v0.9 仕様

この文書は Novara Evidence Bundle v0.9 の仕様を定義する。

目的は、以下を満たす最小フォーマットを固定すること。

- 一日単位で AI 行動の証拠をまとめる
- バイト単位で決定論的に再生成できる
- 単独の zip だけでだれでも検証できる
- 将来の Novara Core や CTK 系拡張にそのまま乗せられる

この v0.9 は二零二五から二零二七向けの実験版であり  
二零四零以降に使われるであろう正式標準の前段階と位置づける。

---

## 一  バンドルの単位

一つの Evidence Bundle は一日と一主体を表す。

- 主体  
  - 人  
  - 組織  
  - サービス  
  のいずれか
- 日付  
  協定世界時での暦日とする  
  例  
  二零二五年十一月十九日

ファイル名

- 主体名を小文字の英数字とハイフンに正規化したもの
- 日付を 西暦年 四桁  月二桁  日二桁 で表したもの
- 例  
  hinata 二零二五年十一月十九日  
  ファイル名  
  hinata 二零二五一一一九 zip

このファイル名は便宜上のものだが  
バンドル内 meta 情報と矛盾してはならない。

---

## 二  zip 内の構造

Evidence Bundle v0.9 は以下の三ファイルを必須とする。

- meta json  
  人間と機械の両方が読めるメタデータ
- aal ndjson  
  Append only の行動ログ  
  一行一記録の Json 行
- anchors json  
  重要ファイルのダイジェスト

zip 内のパスはルート直下とし、サブディレクトリは使用しない。

例

- meta json
- aal ndjson
- anchors json

追加の補助ファイルを入れることは許されるが  
少なくとも上記三つが無ければ v0.9 準拠とは名乗れない。

---

## 三  meta json

meta json は Evidence Bundle 全体のサマリであり  
バンドルレベルの識別と検証条件を持つ。

必須項目

- version  
  文字列  
  本仕様では v0 9 固定
- subject  
  主体の識別子  
  人やサービスの内部 ID など
- date  
  日付  
  例 二零二五一一一九
- timezone  
  主な運用タイムゾーン  
  例 Asia Taipei
- created at  
  バンドル生成時刻 ISO 形式
- producer  
  バンドルを生成したソフトウェア名とバージョン
- chain  
  直前バンドルとの連結情報
  - prev bundle hash  
    直前の zip の全体ハッシュ  
    先頭数十六進数六十四桁
  - position  
    その主体における連番

任意項目

- description  
  自由記述
- tags  
  配列  
  example insurance claim などの用途タグ
- policy id  
  適用されたポリシーの識別子
- model set  
  使用された AI モデル群のバージョン情報

meta json 自体は hash chain の対象外とするが  
anchors json 内でそのダイジェストを持つことができる。

---

## 四  AAL レコード形式

aal ndjson は一行一 Json オブジェクトとする  
各行を AAL レコードと呼ぶ。

必須フィールド

- seq  
  正の整数  
  一から始まり一行ごとに一ずつ増加
- timestamp  
  ISO 形式の時刻  
  協定世界時
- kind  
  記録の種別   
  例  
  llm call  
  payment decision  
  policy update
- actor  
  主な行為主体  
  ai  
  user  
  operator  
  など
- input digest  
  入力に相当する内容のハッシュ  
  sha3 二五六 の十六進表現六十四桁
- output digest  
  出力に相当する内容のハッシュ
- prev hash  
  前のレコードの hash のコピー  
  最初の行のみ null
- hash  
  現在行のダイジェスト

hash の計算方法

一行分のレコードから  
以下の順番でフィールドを取り出し  
Json ではなく素直な連結文字列にして sha3 二五六 を計算する。

- seq を十進数文字列として
- timestamp
- kind
- actor
- input digest
- output digest
- prev hash

その他のフィールドがあってもよいが  
hash 計算に含めるのは上記のみとする。

これにより  
後から説明文などの補助フィールドを追加しても  
証拠としての連鎖は壊れない。

---

## 五  anchors json

anchors json は Evidence Bundle 内の重要ファイルと  
日単位の chain の要約を持つ。

必須項目

- aal  
  - path  
    例 aal ndjson
  - sha3 二五六  
    ファイル全体のハッシュ
- bundle chain  
  - this bundle hash  
    zip 全体のハッシュ
  - prev bundle hash  
    meta json の chain prev bundle hash と一致する値
  - subject  
    meta json の subject と一致
  - date  
    meta json の date と一致

任意項目

- external anchors  
  将来の CTK 系拡張用
  - kind  
    ntp  
    roughtime  
    block hash  
    など
  - location  
    参照先
  - digest  
    その証跡のハッシュ

anchors json 内のハッシュ計算には  
圧縮形式依存の揺れを避けるため  
zip を一定手順で正規化した上で行うことを推奨するが  
v0 9 の必須要件とはしない。

---

## 六  検証手順

Evidence Bundle v0.9 の検証は  
次の順序で行う。

一  zip の展開

- meta json  
- aal ndjson  
- anchors json  
が存在することを確認する。

二  AAL の検証

- 行ごとに Json として妥当であること
- seq が一から始まり一ずつ増加していること
- 各行の hash を本仕様の手順で再計算し  
  記録されている hash と一致すること
- 行二以上では  
  prev hash が直前行の hash と一致すること
- anchors json 内の aal ハッシュが  
  実際の aal ndjson に対する sha3 二五六 と一致すること

三  bundle chain の検証

- anchors json の this bundle hash を  
  zip ファイルに対して再計算し一致を確認
- anchors json と meta json の  
  subject と date が一致していること
- 前日バンドルの zip と anchors json が手元にある場合  
  prev bundle hash が実際の前日ハッシュと一致すること

四  一貫性の確認

- meta json の version が v0 9 であること
- meta json 内の created at が  
  AAL の最終行より後の時刻であること
- 任意の追加検査  
  例  
  ある period の中で seq が連続しているか

検証に必要なものは  
当該 zip  
一般公開されているアルゴリズム  
この仕様  
の三つのみとする。  
外部サービスや秘密鍵への依存は禁止する。

---

## 七  非目標

v0.9 は意図的に  
以下の機能を含まない。

- 署名  
  証拠を誰が出したかの保証は  
  別レイヤに分離する
- 外部チェーンへの書き込み  
  CTK 二系などのアンカーは将来の拡張とする
- プライバシープロテクション  
  匿名化や零知識証明は  
  Evidence Bundle の外側に追加する

これらを切り離すことで  
どの言語でも簡単に実装できる  
小さな検証器を優先する。

---

## 八  バージョニングと互換性

- この文書は Evidence Bundle v0.9 の仕様である
- v1 系では  
  署名  
  外部アンカー  
  サブジェクト間統合などを  
  拡張候補とする
- v0 系と v1 系は  
  zip 内の version フィールドで区別する
- 将来の仕様は  
  v0.9 バンドルをそのまま読み  
  必要に応じて変換できることを目標とする

---

## 九  実装の最小要件

Evidence Bundle v0.9 準拠と主張するには  
少なくとも以下を実装しなければならない。

- 上記構造の zip を生成する機能
- 本仕様に沿った AAL hash chain
- anchors json によるファイルハッシュ固定
- 独立した検証ツール  
  例  
  コマンドラインで  
  zip を渡すと  
  真偽とエラーメッセージを返す

これを越える高度な機能  
例  
ダッシュボード  
クラウド連携  
などは実装者の自由とする。

---

## 十  参照

- Novara リポジトリ  
  Evidence Bundle v0.9 のリファレンス実装
- novara-evidence-bundle-minimal  
  小さな Python 実装  
  テストと例示用 bundle を含む
- roadmap 二零二五 二零二六  
  本仕様が実際にどのような形で使われるかの計画