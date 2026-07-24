---
name: "feature-dev"
displayName: "Feature Development Workflow"
description: "Guides Kiro through repository-aware feature delivery from intent discovery and codebase exploration to architecture, implementation, validation, review, and handoff."
keywords:
  [
    "feature development workflow",
    "repository-aware implementation",
    "codebase exploration",
    "feature architecture",
    "implementation planning",
    "multi-perspective code review",
    "feature delivery",
  ]
author: "sattosh"
---

# Feature Development Workflow

## Overview

Use this power to deliver a non-trivial feature in an existing repository without
jumping prematurely into code. Build an evidence-based understanding of the
request and codebase, resolve consequential ambiguity, choose an architecture,
implement the complete change, validate it, review it from multiple perspectives,
and hand it off with verifiable results.

## When to Use

Use the full workflow when a request:

- adds a feature across multiple files or layers;
- changes architecture, public behavior, storage, security, or integrations;
- has requirements that become clear only after inspecting the repository;
- benefits from comparing implementation approaches; or
- needs a deliberate implementation and quality review cycle.

Use a direct edit-and-validate path instead for a trivial, well-specified change,
a one-line correction, or an urgent narrowly scoped hotfix. Scale the ceremony to
risk and complexity; do not turn a small change into a planning exercise.

Typical activation prompts include:

- "Use the feature development workflow to add OAuth support."
- "Explore this repository before implementing the new dashboard."
- "Design and build this cross-cutting feature end to end."
- "Compare architectures before coding this integration."
- "Plan a repository-aware implementation for this feature."
- "Implement this feature and review it from multiple perspectives."
- "Take this feature from discovery through validated delivery."

## Workflow at a Glance

| Phase                            | Outcome                                                  | Steering guide          |
| -------------------------------- | -------------------------------------------------------- | ----------------------- |
| 1. Intent discovery              | Success criteria, scope, and constraints                 | `steering/discovery.md` |
| 2. Codebase exploration          | Evidence-backed map of relevant code and conventions     | `steering/discovery.md` |
| 3. Clarification                 | Consequential ambiguities resolved or explicitly assumed | `steering/discovery.md` |
| 4. Architecture                  | Recommended design and concrete implementation map       | `steering/delivery.md`  |
| 5. Implementation and validation | Complete, convention-aligned, verified change            | `steering/delivery.md`  |
| 6. Quality review                | High-confidence findings resolved or recorded            | `steering/review.md`    |
| 7. Handoff                       | Results checked against the original request             | `steering/review.md`    |

## Load Steering Progressively

Read only the guide for the current phase, then follow it before moving on:

- **`steering/discovery.md`** — applicability, intent discovery, repository
  exploration, and focused clarification.
- **`steering/delivery.md`** — architecture decisions, approval rules,
  implementation, and validation.
- **`steering/review.md`** — multi-perspective review, remediation, and final
  handoff.

Do not load all three guides up front unless the user explicitly asks for the
entire process in one response. Preserve discoveries and decisions in the active
task context so later phases do not repeat searches or lose constraints.

## Kiro Operating Model

### Track meaningful work

For a multi-step feature, create a `todo_list` before execution and complete each
item immediately when its real outcome is finished. Use
`update_session_information` when the focus changes meaningfully. Keep users
informed with brief progress updates, not a transcript of every tool call.

### Respect session type

- **Vibe session:** Preserve the full interactive workflow. Confirm the initial
  understanding, wait for clarification answers, ask the user to choose an
  architecture, obtain explicit approval before implementation, and ask how to
  handle review findings.
- **Spec session:** Treat approved requirements, design, and tasks as existing
  decisions that satisfy the corresponding confirmation gates. Do not recreate
  them. Explore only what is missing, implement the current approved task, and
  feed newly discovered conflicts back into the spec workflow.
- Recommend a Spec session when the user wants durable requirements, design, and
  task artifacts rather than an in-chat delivery flow.

### Respect autonomy mode

- **Autopilot:** Proceed autonomously between workflow gates, but do not bypass
  the required user confirmations for initial understanding, clarification,
  architecture selection, implementation approval, or review remediation.
- **Supervised:** Hunk approval governs individual edits but does not replace the
  workflow's requirement, architecture, implementation, or remediation gates.
- In every mode, obtain confirmation before high-risk, destructive, production,
  security-sensitive, or irreversible actions.

### Use specialized agents deliberately

- For the full workflow, launch two or three independent repository
  investigations in parallel near the start. Give each investigation a distinct
  lens and require a list of essential files for the primary agent to read.
- Launch two or three independent `general-task-execution` architecture analyses
  in parallel, using minimal-change, clean-boundary, and pragmatic-delivery
  lenses.
- After implementation and validation, launch three independent review passes in
  parallel. Use `semantic_reviewer` for the design and integration account and
  `general-task-execution` for complementary correctness and maintainability
  lenses.
- Keep implementation, validation, finding consolidation, and remediation in the
  primary agent. Do not delegate concurrent mutations to feature files.
- If specialized agents are unavailable, perform the same analysis with
  repository search, focused reads, and local validation. Do not skip the phase.

## Core Rules

1. **Understand before editing.** Inspect project instructions, similar features,
   control and data flow, extension points, and validation conventions first.
2. **Use evidence, not assumptions.** Cite file paths and symbols for repository
   conclusions. Read the key files identified during exploration.
3. **Resolve ambiguity with the user.** Infer facts available in the repository,
   then ask every remaining question that can affect behavior, edge cases,
   integration, compatibility, performance, architecture, or scope. Wait for the
   answers before designing.
4. **Recommend, then confirm.** Present the architecture alternatives, their
   trade-offs, and one recommendation. Ask the user to choose, then obtain
   explicit approval before implementation.
5. **Finish the whole requested feature.** Include integrations, error paths,
   configuration, migrations, and documentation when they are part of the stated
   scope. Avoid unrelated refactoring.
6. **Validate behavior, not just syntax.** Follow repository testing practices
   and run the most relevant tests, checks, build, or smoke test. Add or update
   feature-scoped tests when the chosen architecture, repository conventions, or
   agreed success criteria call for them.
7. **Review high-confidence issues.** Prioritize defects that affect behavior,
   security, maintainability, or explicit project rules. Avoid speculative nits.
8. **Verify the handoff.** Re-read the original request and confirm each success
   criterion against the actual files and validation evidence before claiming
   completion.
