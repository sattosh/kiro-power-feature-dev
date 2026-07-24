# Feature Development Workflow — Kiro Power

[English](README.md) | **日本語**

これは [Kiro](https://kiro.dev) の **power**（機能拡張）です。エージェントを、
いきなりコードを書き始めるのではなく、**リポジトリを理解したうえでの機能開発**へ
と導きます。要求とコードベースを根拠にもとづいて理解し、重要な曖昧さをユーザーと
解消し、アーキテクチャを選び、変更を完成させ、検証し、多角的にレビューしてから
完了を宣言する、という流れを踏ませます。

## ワークフロー

7 つのフェーズからなり、変更のリスクと複雑さに応じて手続きの重さを調整します。

| フェーズ | 成果物 |
| -------- | ------ |
| 1. 意図の把握 | 成功条件・スコープ・制約 |
| 2. コードベース探索 | 関連コードと慣習の根拠つきマップ |
| 3. 明確化 | 重要な曖昧さの解消（または明示的な仮定） |
| 4. アーキテクチャ | 推奨設計と具体的な実装マップ |
| 5. 実装と検証 | 慣習に沿った、検証済みの完全な変更 |
| 6. 品質レビュー | 確度の高い指摘の解消・記録 |
| 7. 引き渡し | 当初の要求に照らした結果確認 |

ステアリング（指針）は段階的に読み込まれ、いまのフェーズに必要なものだけが
コンテキストに入ります。

- **`steering/discovery.md`** — フェーズ 1〜3（適用判断・意図把握・探索・明確化）
- **`steering/delivery.md`** — フェーズ 4〜5（設計判断・承認ゲート・実装・検証）
- **`steering/review.md`** — フェーズ 6〜7（多角的レビュー・修正・引き渡し）

複数ファイルや層をまたぐ機能、アーキテクチャや公開挙動を変える変更、仕様が
曖昧な機能には、この完全なワークフローを使います。ささいで明確な変更のときは、
意図的に「直接編集して検証する」経路に切り替わります。

## インストール

**GitHub から（推奨）**

1. Kiro の powers パネルを開き、**「Add Custom Power」** を選択します。
2. **「Import power from GitHub」** を選びます。
3. リポジトリ URL を入力します: `https://github.com/sattosh/kiro-power-feature-dev`
4. **「Install」** をクリックします。

**ローカルフォルダから**

1. このリポジトリをクローンします。
2. powers パネルで **「Add Custom Power」→「Import power from a folder」** を選びます。
3. クローンしたディレクトリ（`POWER.md` があるフォルダ）を選択します。

## 使い方

インストール後は、要求がキーワードに一致すると power が自動で有効になります。
起動を促すプロンプトの例:

- 「feature development workflow を使って OAuth 対応を追加して」
- 「新しいダッシュボードを実装する前に、このリポジトリを調べて」
- 「この横断的な機能を、最初から最後まで設計して実装して」
- 「この機能を、探索から検証済みの引き渡しまで進めて」

## リポジトリ構成

```
kiro-power-feature-dev/
├── POWER.md              # power マニフェスト + ワークフロー概要（ルート必須）
├── steering/
│   ├── discovery.md      # フェーズ 1〜3
│   ├── delivery.md       # フェーズ 4〜5
│   └── review.md         # フェーズ 6〜7
├── README.md             # 英語
├── README.ja.md          # 日本語（このファイル）
├── LICENSE
└── .gitignore
```

## 動作要件

- Powers に対応した Kiro IDE。

## 謝辞

Anthropic の [Claude Code 向け `feature-dev` プラグイン](https://github.com/anthropics/claude-code/tree/main/plugins/feature-dev)
にインスパイアされています。この power は、そのワークフローを Kiro の power 形式
（`POWER.md` ＋ 段階的に読み込む `steering/` ガイド）へ移植・翻案したものです。

## ライセンス / 作者

MIT License. Author: **sattosh**.
