# Novara

Evidence first な AI ガバナンススタックの実験場。

このリポジトリは  
「一日一束の検証可能な証拠パックを残す」ための  
最小フォーマットとリファレンス実装をまとめたもの。

二零二六年の目的はただ一つ。

二つの問いに  
動くコードと zip で答えを返せる状態にすること。

一  AI がやらかした時に  
    誰が いつ 何を どのポリシーの下でやったのか  
    後から第三者が検算できるか

二  金が動く前に  
    「証拠パックが通っていない支払い」は  
    きちんと止まるか

このリポジトリは  
そのための「最小エビデンスフォーマット」と  
「ひなた自身の人生ログ実験」を載せる場所として使う。

---

## 一  何が入っているか

このリポジトリには  
大きく三つの層がある。

一  フォーマット

二  実装と検証ツール

三  ロードマップと憲法メモ

それぞれの入口は次の通り。

一  Evidence Bundle 仕様

    specs/novara-evidence-bundle-v0.9.md

    一日一主体の zip パックの仕様  
    meta json  
    aal ndjson  
    anchors json  
    の中身と hash chain のルールをここで固定する。

二  実装と例

    src/                Python 参考実装  
    tests/              検証用テスト  
    examples/           実際に生成された bundle 例  
    scripts/            generate と verify の薄いラッパ

    ひなた自身の一日分ログを  
    例として残す予定。

三  ロードマップと憲法寄りのメモ

    docs/roadmap-2025-2026-ja.md  
        大学在学中から二零二六年十月までの  
        ひなた専用ロードマップ v2

    docs/roadmap-2040-checkpoints-ja.md  
        二零二七 二零三〇 二零三三 二零三五までに  
        満たしていないと詰む条件のチェックポイント表

    docs/constitution/  
        Novara Core の原則メモ  
        将来的には novara-core リポジトリ側に寄せていく想定

---

## 二  今のゴール範囲

このリポジトリで二零二六年にやることは  
次の三点に絞る。

一  Evidence Bundle v0 9 を  
    「誰でも再実装できるレベル」で固定する

    仕様  
    参照実装  
    最低限のテスト  
    サンプル zip

二  ひなたの人生 OS として  
    三十から四十五日分を実際に回す

    学習  
    生活  
    小さな SLO 付き実験  
    これらを日次 bundle で残す

三  二つの外部インターフェイスを作る

    一  人間向けの A 四一枚  
        Novara Evidence Bundle の説明と  
        サンプル zip

    二  機械向けの auditor pack v 一  
        検証スクリプト  
        サンプル bundle  
        仕様抜粋

ここまではこのリポジトリだけで完結させる。  
保険や政府や BigTech への展開は  
ロードマップ文書の側で管理する。

---

## 三  使い方の最短ルート

開発環境の前提は Python 三一一 以上。

一  取得

    git clone https://github.com/Novara-developer/Novara.git
    cd Novara

二  セットアップ

    python -m venv .venv
    source .venv/bin/activate
    pip install -e ".[dev]"

三  デモ bundle の生成

    python scripts/generate_demo_bundle.py

四  検証

    python scripts/verify_bundle.py path/to/example.zip

詳細な引数や出力形式は  
後で src と scripts 側の docstring に寄せ  
README では増やさない。

---

## 四  リポジトリ構成案 v0 9

リポジトリの狙いが一目で分かるよう  
トップレベルだけを示す。

Novara  
├── README.md                      このファイル  
├── pyproject.toml                 パッケージ設定  
├── specs/                         形式仕様  
│   └── novara-evidence-bundle-v0.9.md
├── src/                           Python 参考実装  
│   └── novara_evidence/  
├── tests/                         単体テスト  
├── examples/                      サンプル bundle  
├── scripts/                       generate と verify  
├── docs/  
│   ├── roadmap-2025-2026-ja.md  
│   ├── roadmap-2040-checkpoints-ja.md  
│   └── constitution/              原則メモ  
└── .github/                       CI 設定など

この構成に合わないファイルやディレクトリは  
削るか novara-core 側へ移す候補とみなす。

---

## 五  英語話者向けの要約

短い英語だけ残しておく。

Novara is a long horizon experiment in evidence first AI governance.

This repository focuses on a minimal daily evidence bundle format  
and a small Python reference implementation.

For details see

1  specs/novara-evidence-bundle-v0.9.md  
2  docs/roadmap-2025-2026-ja.md  
3  docs/roadmap-2040-checkpoints-ja.md

If you cannot read Japanese  
treat this repo as a reference implementation  
and wait for a future English first core spec in novara-core.