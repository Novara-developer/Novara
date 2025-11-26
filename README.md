# Novara

Evidence first な AI ガバナンススタック  
このリポジトリは「Novara 全体の入口と案内板」。

---

## 概要

Novara は

- AI がお金を動かす
- あとから事故が起きる
- 裁判所や保険会社が「本当にそうだったのか」を検算したい

という場面のための

- 検証可能な証拠パック
- 支払い前の検算レール

をまとめた長期プロジェクト。

ここには

- 全体像
- ロードマップ
- 仕様と他リポジトリへのリンク

だけを置く。  
実際の実装やスキーマは別リポジトリに移す。

---

## English summary

Novara is a long horizon protocol for verifiable AI behaviour and payments.  
This repo is the entry point:

- high level overview
- roadmap
- links to the actual specs and reference implementations

If you want the running code, go directly to the evidence bundle implementation:

- novara evidence bundle minimal

The documents here are mostly in Japanese.  
They exist to keep the original design reasoning legible for the author.

---

## このリポジトリの役割

ここは

- Novara 全体のトップページ
- 他リポジトリへのリンク集
- 二〇四〇までのざっくりしたチェックポイント
- 二〇二五から二〇二六の実行計画

だけを管理する。

証拠フォーマットや SDK のコードは  
novara evidence bundle minimal などに集約していく。

---

## 関連リポジトリ

実装や詳細仕様は次のリポジトリ側に置く。

- novara evidence bundle minimal  
  一日一件の tamper evident な証拠 zip とその Python 参照実装

- novara core  
  ガバナンス原則と長期ロードマップなどテキスト中心の文書

- novara owner spec  
  所有権や資本構造まわりのメモ  
  将来は財団設計ドキュメントに整理予定

- novara civilization os v0001  
  旧来の構想メモ  
  そのままでは使わないが、発想の出典として残しておく

将来的に構成が変わったら、このセクションを真っ先に更新すること。

---

## ディレクトリ構成

このリポジトリの中身はシンプルに保つ。

例

Novara
- README.md               このファイル
- docs
  - roadmap 2025 2026 ja.md     二〇二五から二〇二六の実行計画
  - checkpoints 2040 ja.md      二〇二七 二〇三〇 二〇三三 二〇三五の詰み条件
- specs
  - INDEX.md               仕様ファイルと他リポジトリへのリンク集

コードやスキーマはここに増やさない。  
増えそうになったら別リポジトリに切り出してリンクする。

---

## 二〇二五から二〇二六でやることの要約

詳細は docs 内のロードマップを見る前提で、要点だけを書く。

二〇二五末まで

- Novara evidence bundle minimal を一本にまとめる  
- 一日分の証拠 zip を手ででも生成できる状態にする  
- 過去の失敗と設計変更を failures と iterations として整理する  
- 英語の one pager を一枚用意する

二〇二六年前半

- ひなた自身の生活を Novara で三十から四十五日ログする  
- 観測者を一人入れて、第三者コメント付きの evidence を一回作る  
- 学内ミニ覇権として五から九人の小さな SLO 付き実験を三本行う  
- Novara evidence format v0.9 と auditor pack v1.0 を固める

二〇二六年十月

- スピーチコンテストで  
  evidence format と auditor pack と実ログ実績をまとめて公開する  
- 同日に GitHub と簡易 LP を更新し  
  「真面目な AI は evidence pack を添付しろ」と宣言する

---

## 二〇四〇に向けたチェックポイント

詳細版は docs/checkpoints で管理するが、ルートにも骨だけ置いておく。

- 二〇二七  
  自分と周辺だけでも evidence bundle を日常的に回していること  
  最低一件の実験 PoC に第三者が関わっていること

- 二〇三〇  
  小さい判例の種と保険 PoC のどちらかが動き始めていること  
  Novara 互換の evidence を使った論文かレポートが外部に一つ以上あること

- 二〇三三  
  海外の大学か研究機関のどこかで  
  Novara が名前付きで紹介されていること

- 二〇三五  
  どこか一つの都市か組織で  
  「Novara 互換の証拠が無いと支払いできない」ルールが部分的に走っていること

このどれかに届かなかったら、設計か戦略を全部見直すトリガとする。

---

## 読み始める順番

このリポジトリを初めて開いた人向けの導線。

一  
README をここまでざっと読む

二  
docs/roadmap で  
二〇二五から二〇二六に何をする予定なのかを確認する

三  
実装に興味があるなら  
novara evidence bundle minimal リポジトリに飛ぶ

それ以上の深堀りは各リポジトリ側の README と spec に委ねる。

---

## 連絡とフィードバック

二〇二五年時点では

- ひなた個人による実験段階
- issue も日本語と英語どちらでも可

ただし

- 一般的な AI 話ではなく  
  evidence bundle や検算の話に集中してほしい  
- 大きな提案は別途 design ドキュメントとしてまとめてから議論する