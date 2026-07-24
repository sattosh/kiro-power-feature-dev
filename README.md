# Feature Development Workflow — a Kiro Power

**English** | [日本語](README.ja.md)

A [Kiro](https://kiro.dev) power that guides the agent through **repository-aware
feature delivery** — from intent discovery and codebase exploration to
architecture, implementation, validation, multi-perspective review, and a
verified handoff.

Instead of jumping straight into code, this power makes the agent build an
evidence-based understanding of the request and the repository, resolve
consequential ambiguity with you, choose an architecture, implement the complete
change, validate it, and review it before claiming completion.

## What it does

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

## Installation

**From GitHub (recommended)**

1. In Kiro, open the powers panel and select **"Add Custom Power"**.
2. Choose **"Import power from GitHub"**.
3. Enter the repository URL: `https://github.com/sattosh/kiro-power-feature-dev`
4. Click **"Install"**.

**From a local folder**

1. Clone this repository.
2. In the powers panel, choose **"Add Custom Power" → "Import power from a folder"**.
3. Select the cloned directory (the folder containing `POWER.md`).

## Usage

Once installed, the power activates when your request matches its keywords.
Example activation prompts:

- "Use the feature development workflow to add OAuth support."
- "Explore this repository before implementing the new dashboard."
- "Design and build this cross-cutting feature end to end."
- "Compare architectures before coding this integration."
- "Take this feature from discovery through validated delivery."

## Repository structure

```
kiro-power-feature-dev/
├── POWER.md              # Power manifest + workflow overview (required, at root)
├── steering/
│   ├── discovery.md      # Phases 1–3
│   ├── delivery.md       # Phases 4–5
│   └── review.md         # Phases 6–7
├── README.md             # English (this file)
├── README.ja.md          # Japanese
├── LICENSE
└── .gitignore
```

## Requirements

- Kiro IDE with Powers support.

## Acknowledgements

Inspired by Anthropic's [`feature-dev` plugin for Claude Code](https://github.com/anthropics/claude-code/tree/main/plugins/feature-dev).
This power adapts that workflow into the Kiro power format (`POWER.md` + progressive `steering/` guides).

## License

MIT License. Author: **sattosh**.
