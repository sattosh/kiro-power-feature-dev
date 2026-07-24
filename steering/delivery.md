# Architecture, Implementation, and Validation

Use this guide for phases 4–5 after discovery has established the feature
contract, repository evidence, and any required user decisions.

## Phase 4 — Architecture and Implementation Map

### 1. Compare architecture lenses in parallel

For the full workflow, launch two or three independent
`general-task-execution` agents in one parallel batch. Give each agent the same
confirmed constraints and repository evidence but a different optimization lens:

- **minimal change:** maximize reuse and reduce blast radius;
- **clean boundary:** optimize separation, testability, and long-term ownership;
- **pragmatic delivery:** preserve key boundaries while limiting new machinery.

Use two agents only when repository constraints make one lens materially
duplicative; otherwise use all three. Submit all agent calls before awaiting
results so the analyses actually run in parallel.

Do not delegate the final decision. The primary agent must compare the results,
check them against repository evidence, and own the recommendation. If sub-agents
are unavailable, evaluate the same lenses directly.

### 2. Produce a concrete design

The design should be specific enough that implementation does not require fresh
architectural invention. Include:

- objective and confirmed constraints;
- chosen approach and why it fits existing patterns;
- alternatives considered and their material trade-offs, if any;
- components and responsibilities;
- interfaces, schemas, state transitions, and data flow;
- exact files or modules to create or modify;
- error, security, compatibility, migration, and rollback behavior;
- implementation sequence, testing approach, and validation strategy.

Use file paths and symbol names supported by repository evidence. Label proposed
new names as proposals rather than existing facts.

### 3. Apply the architecture and implementation gates

For the full workflow in a Vibe session, complete both gates before editing:

1. Present a brief summary of each architecture approach, its material trade-offs,
   the primary agent's recommendation and rationale, and the concrete
   implementation differences. Ask which approach the user prefers and wait for
   the answer.
2. After the user selects an approach, restate the resulting implementation map
   and ask for explicit approval to begin implementation. Wait for that approval.

If the user delegates the architecture choice or says "whatever you think,"
recommend one approach and ask for explicit confirmation. Do not treat delegation
as confirmation.

The original feature request, Autopilot mode, a safe default, or Supervised hunk
approval does not satisfy these gates. A small change following the direct
edit-and-validate path does not require the full architecture ceremony.

In a Spec session, an approved design satisfies architecture selection, and an
approved implementation task being executed in the current request satisfies the
implementation gate. If repository evidence conflicts with either artifact,
return to the user for a decision. Obtain additional confirmation for persistent
data, authentication, authorization, privacy, billing, production infrastructure,
unusual dependencies, breaking changes, or irreversible actions.

### 4. Refine the task list

Translate the design into ordered, outcome-based implementation tasks. Respect
dependencies: establish contracts and data structures before consumers, core
behavior before adapters, and implementation before validation and review.

For multi-file scaffolding, first communicate the intended structure, create the
minimal coherent skeleton, then fill in complete working behavior. Do not leave
stubs or placeholder implementations at handoff.

### Phase 4 exit check

Begin implementation only when the chosen approach, affected components,
integration behavior, build sequence, testing approach, and validation strategy
are clear, the user has selected the architecture, and explicit implementation
approval has been received or satisfied by an approved Spec task.

## Phase 5 — Implementation

### 1. Prepare the edit

Before changing an existing file, read enough of it to preserve its style and
invariants. Reuse known repository patterns rather than introducing a new
abstraction by preference alone. Keep the requested behavior and its necessary
integration in scope; exclude opportunistic cleanup.

Choose the safest available operation:

- targeted edits for localized changes;
- `semantic_rename` for repository-wide symbol renames;
- `smart_relocate` for file moves that require import updates;
- one coherent write for each genuinely new file.

Batch independent reads and validations, but do not parallelize dependent edits
or multiple mutations to the same file.

### 2. Implement in dependency order

A typical sequence is:

1. contracts, schemas, or domain types;
2. core behavior and state transitions;
3. persistence or external adapters;
4. API, command, event, or UI entry points;
5. configuration, migrations, and compatibility handling;
6. requested documentation and integration updates.

Adjust this sequence to the repository. Preserve existing public behavior unless
the feature contract explicitly changes it. Handle failure paths and cleanup as
part of implementation, not as optional review work.

### 3. Follow repository and platform constraints

- Obey applicable steering and contribution guidance.
- Pin dependency versions when adding a dependency, explain why it is needed,
  and flag suspicious or unusual package names.
- Do not transmit repository code, secrets, or user data to external services.
- Use non-interactive, platform-appropriate commands.
- Do not start long-running servers or watchers through blocking command tools.
- Do not create commits, push branches, or open pull requests unless requested.
- Never bypass hooks or use destructive Git operations without explicit consent.
- Follow established testing practices. Add or update feature-scoped tests when
  the chosen architecture, nearby features, project policy, or an agreed success
  criterion calls for them. Treat this coverage as part of the implementation,
  not as separate scope requiring another approval round.

After each implementation outcome is real, complete its task-list item
immediately and record the files changed.

### 4. Validate at the narrowest useful scope

Derive commands from package scripts, build files, contribution docs, and nearby
examples. Prefer this order:

1. focused tests for changed behavior;
2. affected package type checking or static analysis;
3. lint or formatting checks;
4. affected package build;
5. a minimal non-interactive smoke test.

Run only checks that exist and are relevant. For expensive monorepos, start with
the affected package and expand if shared contracts or failures justify it.

A successful command is evidence, not proof. Inspect whether it actually covered
the requested behavior and whether generated files, snapshots, schemas, or
migrations are consistent.

### 5. Resolve validation failures

When a check fails:

1. determine whether the failure is caused by the change, pre-existing, or an
   environment limitation;
2. fix change-caused failures and rerun the smallest relevant check;
3. avoid editing unrelated code merely to make a broad check green;
4. report pre-existing or environmental blockers with command and evidence;
5. never claim a check passed if it was skipped, timed out, or only partially ran.

Do not move to quality review while a known change-caused validation failure
remains unresolved.

### Phase 5 exit check

Proceed when the requested feature is integrated, no deliberate placeholder
remains, relevant validation has passed or has a clearly evidenced external
blocker, and the actual diff is ready for behavioral review.
