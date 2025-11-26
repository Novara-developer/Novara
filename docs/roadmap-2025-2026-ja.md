# Novara 2025-2026 ロードマップ v2（ひなた用）

この文書は「ひなた個人として 2025-2026 年にやること」を  
Novara 覇権ロードマップと接続した形で固定する。

目的は二つ。

- 2026 年 10 月までに「撃てる弾」と「失敗ログ」をそろえること  
- その弾を NUS や BigTech にそのまま提出できる形にしておくこと

---

## 0. 2026 年 10 月時点でそろえるもの

2026 年 10 月頭（スピーチコンテスト想定）までに、最低限そろっていないといけないもの。

技術

- Novara Evidence Bundle v0.9（日本語仕様書、英語要約）
- NovaraAI API v1.0
  - route
  - audit
  - report の基本スキーマ
- auditor_pack v1.0
  - サンプル bundle
  - verify レポート
  - 短い解説スライド
  - ひなた用 Pocket Judge（ローカル検証スクリプト）

運転実績

- Anchors 90 日連続
- 小さくてもいいので P2P 三百件規模の決定ログ
- 学内ミニ覇権
  - ひなた以外の人が Novara 経由で勉強や作業を回している実例

外向けの接続

- BigTech か 大学 か 日本か台湾のどこか
  - メールでもオンライン面談でも一度は接続済み
- 公開リポジトリ
  - Novara メインリポ
  - novara-evidence-bundle-minimal
- 公開ドキュメント
  - このロードマップ
  - Evidence Bundle v0.9

英語と学歴

- TOEIC 1 回以上受験、六百点レンジ
- 2026 年以降の転校先を見据えた時間割に乗り換え

---

## 1. フェーズ一覧

ざっくりした時間軸とテーマはこう置く。

- Phase 0 〜2025 年 12 月末  
  個人作品から「標準プロトコル屋」への立ち上げ
- Phase 1 2026 年 1〜3 月  
  Novara-core 心臓と人生 OS 一号機
- Phase 2 2026 年 4〜6 月  
  学内ミニ覇権と複数 LLM ルーター
- Phase 3 2026 年 7〜9 月  
  Evidence Format v0.9 と auditor_pack v1.0
- Phase 4 2026 年 10 月  
  スピコンで Novara フォーマット宣言
- その後 2026 年 11 月以降  
  転校先での Phase A（NUS 出願モードの起動）

以下、各フェーズで「やること」と「エビデンス」を固定する。

---

## Phase 0 〜2025 年 12 月末  
個人作品から「標準プロトコル屋」へ

テーマ  
「バラバラなコード置き場」ではなく  
「標準と仕様を配る表札リポジトリ」に切り替える。

技術

- Novara リポ構成の再定義
  - ルートに README
  - docs/ にこのロードマップ
  - specs/ に Evidence Bundle v0.9
- novara-evidence-bundle-minimal への分離
  - コードと仕様をそちらに集約
- Artifact Index を作成
  - どのリポのどのファイルが何の証拠かを一覧化

設計ログ

- failures.md
  - 古い AAL や署名設計で失敗した理由を具体的に書く
- iterations.md
  - v0.1 から v0.2 への変更理由
  - どの妥協をしたか
- open-questions.md（日英）
  - マルチ TEE
  - 保険との接続
  - 教育以外ユースケースなど、未解決ポイント一覧

英語

- 1 日二〜三時間
  - 文法総復習
  - B1 レベル単語
  - 聴解
- 目標
  - 模試で TOEIC 四百〜四百五十レンジ

アウトリーチの下準備

- Novara One-Pager（英語）
- シンプル LP
- テンプレメール三種
  - 研究者向け
  - 企業向け
  - 政府・大学向け
- outreach-log テンプレ
  - 宛先
  - 日付
  - 送った内容の要約
  - 返信の有無

エビデンス

- github.com/Novara-developer/Novara の履歴
- failures.md と iterations.md
- novara-evidence-bundle-v0.9.md のコミット
- Novara One-Pager の PDF か markdown

---

## Phase 1 2026 年 1〜3 月  
Novara-core 心臓と人生 OS 一号機

テーマ  
「ひなた専用 OS」を本当に 30 日以上回し切る。

技術

- Novara-core API の骨組み
  - POST /api/aal/ingest
  - GET  /api/aal/verify/:hash
  - POST /api/pay/decide
  - GET  /api/metrics/solo.json
- llm_profiles.json
  - GPT-5.1-thinking を tier A, priority 1
  - Claude, Gemini, Grok も役割付きで定義
- /novara-ai/route と /novara-ai/audit の骨
  - goal と constraints から steps を出す
  - tool_assign と plan_hash を刻む
- novara-watchdog v0
  - 新しい bundle を見つけたら verify してレポートを書く

人生 OS 運転

- 毎日
  - 今日のゴールを /aal/ingest に刻む
  - 結果と自己評価を /pay/decide で APPROVE か HOLD にする
  - 大きい決定は /novara-ai/route 経由でプランを残す
- 目標
  - Anchors 30〜45 日連続

観測者プログラム v0

- 家族か友人一人に AAL ダッシュボードを見せる
- observer_feedback.ndjson を週 1 回書いてもらう
- コメント例
  - この週は HOLD が多い
  - 体調が悪そう
  - 勉強の集中度が上がっている、など

英語

- 1 日三〜四時間
  - TOEIC 本番対策
- 目標
  - 春〜初夏の本番で 550〜600 レンジ

アウトリーチ第 1 波

- 月十通ペースでメール
  - 台湾の教授
  - NUS のラボ
  - 教育系 SaaS
- 全て outreach-log に記録
- 返信ゼロでも「撃った弾の数」がエビデンス

エビデンス

- Anchors 連続日数のグラフ
- observer_feedback.ndjson
- /metrics/solo.json の履歴
- 送信済みメール一覧

---

## Phase 2 2026 年 4〜6 月  
学内ミニ覇権と複数 LLM ルーター

テーマ  
「ひなただけの OS」から  
「学内の数人が使う OS」へ拡張する。

技術

- 学内ミニ覇権 5〜9 人
  - 勉強ログと返金 SLO の小さな実験
  - Before/After とコメント付きケース 3 本
- 複数 LLM ルーター 0.9
  - complexity_score, risk_score を導入
  - 難しい案件や高リスクは GPT と Claude
  - 情報収集は GPT と Gemini
  - 雑談寄りは GPT か Grok
- novara-bench v0.1
  - 十〜二十問の固定ベンチ
  - CTK-2 説明や refusal など
  - kind: "llm_regression" で AAL に記録
- novara-incidents v0
  - 小さな失敗やバグを事件扱いにし、フル bundle で一、二件公開

英語

- TOEIC 本番で 600 台を狙い、終わったら TOEIC から撤退
- IELTS 準備に少しずつ移行

アウトリーチ第 2 波

- 日本帰省のタイミングで
  - 高校
  - 塾
  - 予備校 に PoC 打診
- メール先も拡張
  - 日本の省庁
  - 教育系スタートアップ
  - 令和の虎 用企画書の下書き

エビデンス

- 学内メンバーそれぞれの bundle
- SLO と返金実績
- novara-bench のスコア推移
- incidents フォルダの bundle とタイムライン

---

## Phase 3 2026 年 7〜9 月  
Evidence Format v0.9 と auditor_pack v1.0

テーマ  
「とりあえず動いている」から  
「他人が検証できるフォーマット」へ。

技術

- Novara Evidence Bundle v0.9
  - specs/novara-evidence-bundle-v0.9.md を日本語で固定
  - 英語サマリを同ファイルか別ファイルで添付
- NovaraAI API v1.0
  - route と audit のスキーマを固定
  - v0.x から v1.0 への変更理由を書く
- auditor_pack v1.0
  - サンプル bundle
  - verify レポート
  - 短い解説スライド
  - ローカルで動く検証スクリプト

英語

- 夏は英語に寄せて一日六時間レベル
  - IELTS リスニング
  - リーディング
  - ライティングの型
- 目標
  - IELTS 5.5〜6.0 レンジ

アウトリーチ第 3 波

- NUS, NTU, SMU の教授へ
  - Evidence Format v0.9 と auditor_pack を添付して再アタック
- BigTech へ
  - Google, Microsoft, OpenAI, Anthropic, GitHub などに
  - 内部ログや Evidence Pack のフォーマット案として提案
- 令和の虎
  - 応募に必要な資料をここでほぼ完成させる

エビデンス

- specs/novara-evidence-bundle-v0.9.md コミット
- auditor_pack.zip
- 各社へのメールと返信ログ

---

## Phase 4 2026 年 10 月  
スピーチコンテストと Novara フォーマット宣言

テーマ  
「ひなた用プロトタイプ」から  
「未来の標準候補として殴り込む」。

やること

- スピーチで扱う中身
  - 事故例
  - Evidence Bundle v0.9
  - NovaraAI API v1.0
  - Anchors と P2P 実績グラフ
- 同時に行う公開
  - GitHub の整えたリポジトリ
  - LP
  - auditor_pack v1.0
- 宣言文の中身
  - 真面目な AGI や ASI は
    - Novara 互換 Evidence Pack を添付せよ
    - そうでないものは「証拠なし」と見なす

エビデンス

- スピーチ動画
- スライド
- 公開された GitHub と LP
- その日の bundle と verify レポート

---

## 2. 2026 年 11 月以降の入口だけメモ

この文書は「2025-2026 ロードマップ」なので詳細は書かない。  
ただし、ここまで終わった時点で次に踏み出すフェーズだけ固定する。

- Phase A 2026 年 11 月〜  
  転校先で GPA と電子証拠を両方積む一年
  - GPA 三点七〜四点ゼロ
  - IELTS 六点五を一回出しておく
  - Novara を卒研か Independent Study に乗せる
  - 小さめ論文一件と Evidence Pack を添えて公開

ここから先は roadmap-2040-checkpoints-ja.md で  
二〇四〇覇権のチェックポイントとつなげる。