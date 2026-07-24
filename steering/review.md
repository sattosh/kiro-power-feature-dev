# Quality Review and Handoff

Use this guide for phases 6–7 after implementation and targeted validation. The
review must evaluate behavior and integration, not merely restate changed files.

## Phase 6 — Multi-Perspective Quality Review

### 1. Establish the review scope

Review the actual change set: unstaged and staged diffs, new files, generated
artifacts, and any relevant base comparison requested by the user. Include the
confirmed feature contract, architecture decision, repository rules, and
validation results as review context.

Do not report unrelated pre-existing issues as feature regressions. If an old
issue blocks safe delivery, identify it explicitly as pre-existing and explain
the interaction.

### 2. Launch three review passes in parallel

For the full workflow, launch three independent review passes in one parallel
batch, one for each lens in the next section. Give every reviewer the same
feature contract, architecture decision, actual change set, repository rules,
and validation evidence, but a different focus.

Use `semantic_reviewer` for the repository-conventions and integration lens.
Use two `general-task-execution` agents for the correctness and maintainability
lenses. If `semantic_reviewer` is unavailable, use three
`general-task-execution` reviews instead. Submit every review call before
awaiting results so the reviews actually run in parallel.

Do not use duplicate prompts. Agents provide evidence and findings; the primary
agent consolidates, verifies, and decides what to fix. If sub-agents are
unavailable, inspect the diff and relevant surrounding code directly through all
three lenses. A small change following the direct edit-and-validate path may use
one focused self-review instead of the full three-pass workflow.

### 3. Review through three lenses

#### Correctness, safety, and security

Check:

- feature behavior against every success criterion;
- edge cases, error propagation, retries, cleanup, and state consistency;
- nullability, concurrency, ordering, and partial failure;
- authorization, input validation, secret handling, privacy, and injection risk;
- migration compatibility, rollback behavior, and external contract changes;
- whether validation meaningfully exercised the changed behavior.

#### Simplicity and maintainability

Check:

- whether the design is simpler than equally correct alternatives;
- duplication, unnecessary indirection, hidden coupling, and leaky abstractions;
- names, module responsibilities, control flow, and comments;
- testing approach, meaningful feature coverage, and test maintainability;
- performance or resource costs introduced by the design;
- whether complexity is justified by a stated requirement.

#### Repository conventions and integration

Check:

- explicit project instructions and established nearby patterns;
- boundaries, dependency direction, imports, configuration, and lifecycle hooks;
- platform, accessibility, observability, and localization conventions where
  applicable;
- completeness across entry points, adapters, generated artifacts, schemas,
  migrations, and documentation required by scope.

### 4. Filter and format findings

Report only actionable, high-confidence issues. Use approximately an 80/100
confidence threshold unless project review rules specify otherwise. Do not pad
the review with preferences or speculative edge cases.

For each finding provide:

- severity and confidence;
- exact file and line or symbol;
- concrete user or system impact;
- repository evidence or violated invariant;
- a specific minimal fix.

Group findings by severity. If no high-confidence issue exists, say so plainly
and summarize the reviewed risks and validation evidence.

### 5. Ask how to handle review findings

After consolidating the review, present the highest-severity findings and the
primary agent's remediation recommendation. Ask the user whether to:

- fix the findings now;
- defer them for later; or
- proceed without fixing them.

Wait for the user's decision before changing code. Autopilot mode and Supervised
hunk approval do not replace this remediation gate. If no high-confidence finding
exists, state that plainly and proceed to handoff without manufacturing a
decision.

Apply only the selected remediation. Ask a follow-up question when a requested
fix changes product behavior, broadens scope, selects a material trade-off, or
requires a high-risk action.

After fixes:

1. inspect the updated diff;
2. rerun the checks affected by the fix;
3. confirm that the fix did not invalidate the architecture or success criteria;
4. repeat focused review only for the changed concern, not the entire discovery
   process.

Record intentionally deferred findings and why they do not block delivery.

### Phase 6 exit check

Move to handoff when no unresolved in-scope high-severity defect remains,
remediation has been revalidated, and any deferred issue is explicit rather than
silently ignored.

## Phase 7 — Verified Handoff

### 1. Re-read the original request

Do not summarize from memory. Compare the actual result with the user's concrete
success criteria, including requested behavior, values, paths, formats, and
scope boundaries. Check the real files and outputs needed to substantiate each
claim.

### 2. Close task and session state accurately

Complete remaining `todo_list` items only after their outcomes are verified.
Update `update_session_information` to completed when the overall request is
finished, or waiting when an external user decision is still required. Include
all modified paths in task context.

Do not create a Git commit or push unless the user explicitly requested it.

### 3. Present a concise results-first handoff

Include only decision-useful information:

- **Built:** the observable feature behavior;
- **Key decisions:** architecture or scope choices that affect future work;
- **Changed:** important created or modified files;
- **Validation:** exact checks run and their outcomes;
- **Review:** high-confidence issues fixed, absent, or deliberately deferred;
- **Limitations or next steps:** only real remaining work or unverified criteria.

State skipped or blocked validation explicitly. Distinguish "not run" from
"failed" and "passed." Never claim the task is complete solely because a command
exited successfully.

### 4. Keep next steps proportional

Suggest follow-up work only when it is useful and outside the current request,
such as rollout monitoring, broader integration testing, a migration window, or
future extensibility. Do not leave required in-scope work as an optional next
step.

## Recovery Paths

### Exploration found the request conflicts with the repository

Return to focused clarification. Present the conflicting evidence and smallest
set of viable choices. Do not force the original wording into an incompatible
architecture.

### Implementation exposed a design flaw

Pause edits, update the architecture decision and affected tasks, then continue
from the earliest invalidated step. Do not repeat unaffected discovery.

### Review found widespread unrelated debt

Separate feature-blocking issues from general debt. Fix only what is required for
a safe feature unless the user expands scope.

### Validation cannot run in the environment

Use the next-best static or smoke check, inspect the relevant behavior manually,
and report exactly what remains unverified and how the user can verify it.
