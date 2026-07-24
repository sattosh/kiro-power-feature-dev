# Feature Development Workflow — a Kiro Power

A [Kiro](https://kiro.dev) power that guides the agent through **repository-aware
feature delivery** — from intent discovery and codebase exploration to
architecture, implementation, validation, multi-perspective review, and a
verified handoff.

Instead of jumping straight into code, this power makes the agent build an
evidence-based understanding of the request and the repository, resolve
consequential ambiguity with you, choose an architecture, implement the complete
change, validate it, and review it before claiming completion.

---

## English

### What it does

The power drives a seven-phase workflow and scales the ceremony to the risk and
complexity of the change:

| Phase | Outcome |
| ----- | ------- |
| 1. Intent discovery | Success criteria, scope, and constraints |
| 2. Codebase exploration | Evidence-backed map of relevant code and conventions |
| 3. Clarification | Consequential ambiguities resolved or explicitly assumed |
| 4. Architecture | Recommended design and concrete implementation map |
| 5. Implementation & validation | Complete, convention-aligned, verified change |
| 6. Quality review | High-confidence findings resolved or recorded |
| 7. Handoff | Results checked against the original request |

Steering guidance is loaded progressively so only the guide for the current
phase enters context:

- **`steering/discovery.md`** — applicability, intent discovery, repository exploration, and focused clarification (phases 1–3).
- **`steering/delivery.md`** — architecture decisions, approval gates, implementation, and validation (phases 4–5).
- **`steering/review.md`** — multi-perspective review, remediation, and final handoff (phases 6–7).

Use the full workflow for a feature that spans multiple files or layers, changes
architecture or public behavior, or is underspecified. For a trivial, well-scoped
change, the power intentionally falls back to a direct edit-and-validate path.

### Installation

**From GitHub (recommended)**

1. In Kiro, open the powers panel and select **"Add Custom Power"**.
2. Choose **"Import power from GitHub"**.
3. Enter the repository URL: `https://github.com/sattosh/kiro-power-feature-dev`
4. Click **"Install"**.

**From a local folder**

1. Clone this repository.
2. In the powers panel, choose **"Add Custom Power" → "Import power from a folder"**.
3. Select the cloned directory (the folder containing `POWER.md`).

### Usage

Once installed, the power activates when your request matches its keywords.
Example activation prompts:

- "Use the feature development workflow to add OAuth support."
- "Explore this repository before implementing the new dashboard."
- "Design and build this cross-cutting feature end to end."
- "Compare architectures before coding this integration."
- "Take this feature from discovery through validated delivery."

### Repository structure

```
kiro-power-feature-dev/
├── POWER.md              # Power manifest + workflow overview (required, at root)
├── steering/
│   ├── discovery.md      # Phases 1–3
│   ├── delivery.md       # Phases 4–5
│   └── review.md         # Phases 6–7
├── README.md
├── LICENSE
└── .gitignore
```

### Requirements

- Kiro IDE with Powers support.

---

## 日本語

### 概要

これは [Kiro](https://kiro.dev) の **power**（機能拡張）です。エージェントを、
いきなりコードを書き始めるのではなく、**リポジトリを理解したうえでの機能開発**へ
と導きます。要求とコードベースを根拠にもとづいて理解し、重要な曖昧さをユーザーと
解消し、アーキテクチャを選び、変更を完成させ、検証し、多角的にレビューしてから
完了を宣言する、という流れを踏ませます。

### ワークフロー

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

### インストール

**GitHub から（推奨）**

1. Kiro の powers パネルを開き、**「Add Custom Power」** を選択します。
2. **「Import power from GitHub」** を選びます。
3. リポジトリ URL を入力します: `https://github.com/sattosh/kiro-power-feature-dev`
4. **「Install」** をクリックします。

**ローカルフォルダから**

1. このリポジトリをクローンします。
2. powers パネルで **「Add Custom Power」→「Import power from a folder」** を選びます。
3. クローンしたディレクトリ（`POWER.md` があるフォルダ）を選択します。

### 使い方

インストール後は、要求がキーワードに一致すると power が自動で有効になります。
起動を促すプロンプトの例:

- 「feature development workflow を使って OAuth 対応を追加して」
- 「新しいダッシュボードを実装する前に、このリポジトリを調べて」
- 「この横断的な機能を、最初から最後まで設計して実装して」
- 「この機能を、探索から検証済みの引き渡しまで進めて」

### ライセンス / 作者

MIT License. Author: **sattosh**.
