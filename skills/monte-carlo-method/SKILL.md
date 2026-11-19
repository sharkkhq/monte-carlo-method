---
name: monte-carlo-method
description: Engineering discipline for coding agents. Apply when designing, implementing, refactoring, reviewing, or testing software. Prioritizes clear declarative APIs, behavior-focused tests, coherent acyclic organization, minimal justified complexity, verified outcomes, and stewardship of the workspace and version history.
---

# The Monte Carlo Method

**Build the simplest coherent system that fulfills the actual contract. Make intent obvious, complexity accountable, and results verifiable.**

**Stewardship is paramount.** The agent is responsible not only for the code it produces, but for the condition of the repository, workspace, and history it leaves behind. That responsibility extends to every subagent it delegates to.

Apply these rules with judgment. A trivial edit does not require an architectural review. Project-specific constraints take precedence when explicit; surface meaningful conflicts rather than quietly overriding them.

## Stewardship of the codebase and workspace

- **Leave things better, never messier.** Own the full lifecycle of your work: temporary files, generated output, experiments, worktrees, branches, processes, caches, documentation, and obsolete artifacts. Clean up what you create when it is no longer needed; retain intentional, useful outputs. Do not delete user data or unrelated pre-existing material.
- **Inspect version-control state before changing anything.** Identify the repository root, current branch, existing modifications, untracked files, and any relevant project workflow. Treat pre-existing work as belonging to someone else unless explicitly told otherwise.
- **Use version control as a tool for understanding and accountability.** Consult history and diffs when useful, keep changes focused and reviewable, and check the final diff and status. Prefer small, coherent commits at meaningful milestones when commits are expected or authorized by the workflow; do not manufacture commits for every edit.
- **Never silently rewrite or discard history or work.** Do not force-push, hard-reset, clean indiscriminately, amend another author's commit, or overwrite unrelated changes without explicit authorization. Do not stage or commit another contributor's changes. Preserve provenance and explain any necessary destructive operation first.
- **Keep working trees and branches intentional.** Avoid stray files, accidental lockfile churn, generated binaries, scratch scripts, abandoned branches, and untracked artifacts. Update ignore rules only when broadly warranted; do not hide genuine source files or mistakes behind ignores.
- **Delegate responsibility, not chaos.** Give subagents explicit scope, file ownership or non-overlapping work areas, expected deliverables, verification requirements, and cleanup obligations. Coordinate shared files; integrate and inspect their work before accepting it. The parent agent remains accountable for all delegated changes.
- **Keep version-control ownership clear across agents.** Prefer one integrator responsible for staging, commits, merges, and final history; subagents normally modify their assigned files and report diffs and checks rather than independently committing. If independent branches or worktrees are warranted, define integration and cleanup up front.
- **Respect the existing environment.** Avoid unnecessary dependency installation, global configuration changes, destructive commands, background processes, or machine-wide side effects. Close processes and release resources that your work started or acquired.
- **Finish with an honest handoff.** Report meaningful changes, verification, repository state, commits if any, and intentional leftovers or blockers. A clean handoff matters as much as working code.

**Stewardship test:** Could the next contributor resume work immediately, understand what changed, and trust that nothing unrelated was disturbed?

## 1. Understand before acting

- Identify the user's actual goal, observable success criteria, constraints, and affected boundaries.
- Inspect the existing implementation and conventions before choosing a design.
- Distinguish facts from assumptions; surface material ambiguity and consequential tradeoffs. Ask only when an incorrect guess would matter and cannot be reasonably resolved.
- Recommend a simpler approach when one exists. Do not implement a request's implied machinery when its intended outcome can be achieved more directly.
- For nontrivial work, use a short plan with explicit verification points. Do not substitute planning for doing.

## 2. Make complexity earn its place

- Choose the smallest *conceptual* solution, not necessarily the one with the fewest lines.
- Avoid speculative features, generic frameworks, unnecessary layers, knobs, factories, and one-use abstractions.
- Prefer direct control flow, visible data movement, explicit ownership, and local reasoning.
- Consolidate genuine repetition, but do not erase meaningful differences to force reuse.
- Preserve necessary edge-case handling. Do not manufacture defenses for impossible states, but do handle plausible failures at the correct boundary.
- A new abstraction must simplify multiple real uses, enforce a meaningful invariant, or isolate genuine volatility.

## 3. Make interfaces speak plainly

- Give public APIs, and preferably internal APIs, simple, descriptive, unsurprising English or naturalized-English names.
- Name things for **what they mean or do**, not how clever their implementation is. Prefer domain vocabulary over internal jargon, arbitrary abbreviations, and overloaded metaphors.
- Use the same word for the same concept; use distinct words for distinct concepts. Follow established project or domain terminology where it would otherwise confuse users.
- Prefer declarative interfaces: callers state the desired result or intent; implementations own incidental sequencing and mechanics.
- Expose a small coherent set of operations. Make common actions obvious and safe, with defaults that match ordinary use.
- Distinguish commands from queries where practical: a query observes; a command changes state. Make side effects and expensive behavior discoverable.
- Make invalid states difficult to represent, but do not hide essential state or failure modes behind magical behavior.
- Prefer concrete domain types and explicit contracts over ambiguous strings, booleans, and positional arguments when confusion is likely.
- Do not create a DSL merely to appear declarative. A plain function with clear arguments is often the best API.

**API smell:** `mgr.exec(op, opts, true)`

**Clearer intent:** `service.start("cache")` or `services.ensure_running("cache")` — choose names that reflect the *actual* contract, not cosmetic preferences.

**Naming test:** Can a new contributor infer a call's purpose, important effects, and result without reading its implementation?

## 4. Organize by responsibility and dependency direction

- Group code by coherent purpose, ownership, and change reasons, not arbitrary file-size quotas or excessive taxonomies.
- Give modules clear boundaries. A module should have a comprehensible reason to exist and a narrow public surface.
- Dependencies should generally flow in one direction: higher-level policy depends on lower-level capabilities, not vice versa.
- Prefer acyclic module and package dependency graphs. Resolve cycles by relocating shared concepts, clarifying ownership, or introducing a small boundary interface only when justified.
- Keep data flow and lifecycle ownership legible. Avoid implicit global coordination, concealed mutation, and unrelated modules reaching into each other's internals.
- Favor composition over inheritance or elaborate plugin mechanisms unless the problem establishes their value.
- Keep related code close enough to reason about; avoid splitting simple operations across many files.
- When a cycle is unavoidable or deliberately chosen, document why, constrain it, and verify its consequences. Do not add complexity just to satisfy a diagram.

**Architecture test:** Can someone identify who owns a behavior, where to change it, and what depends on it without tracing a maze?

## 5. Test contracts, not construction details

- Write tests against observable behavior, documented contracts, domain invariants, and meaningful failures.
- Prefer tests that survive correct refactoring: changing private helpers, call order, internal data structures, or algorithms should not break them unless those details are part of the contract.
- Test through the narrowest stable boundary that demonstrates the desired behavior, using unit, integration, or end-to-end tests as appropriate.
- Use realistic inputs and outputs. Cover representative normal cases, boundaries, errors, and regressions.
- For a bug, reproduce the failing behavior where feasible before fixing it. For refactors, establish existing behavior before changing internals.
- Avoid mock-heavy tests that merely restate implementation choreography. Mock external effects or expensive/nondeterministic boundaries when necessary; do not mock the behavior being tested.
- Tests should be deterministic, understandable, independent, and proportionate to risk. Do not chase coverage percentages at the expense of useful assertions.
- Test performance, ordering, resource lifetime, concurrency, or internal invariants specifically when they are *actual requirements*.

**Test smell:** “The method calls helper A, then helper B exactly once.”

**Behavior test:** “Given an expired session, the request is rejected and no state change is committed.”

## 6. Change surgically; finish completely

- Keep edits tied to the user's request and the acceptance criteria. Match the existing style unless a style change is part of the task.
- Fix root causes when practical. Do not hide a broken invariant with retries, flags, special cases, or tests that cement the bug.
- Avoid drive-by rewrites, cleanup, formatting, dependency updates, and unrelated improvements.
- Remove artifacts made obsolete by *your change* (unused imports, abandoned code paths, outdated related tests). Report pre-existing unrelated issues separately.
- Preserve compatibility when required; explicitly identify breaking changes rather than silently introducing them.
- Run the most relevant available checks: tests, build, static analysis, functional execution, or focused inspection. Never claim verification you did not perform.
- Report what changed, what was verified, and any material remaining limitations. Keep the report proportional to the work.

## 7. Engineer for measured reality

- Start with correct algorithms, sensible complexity, good data locality, and simple resource lifetimes.
- Identify actual workload, bottleneck, and performance target before specialized optimization.
- Measure representative cases; distinguish benchmarks from production behavior and regressions from noise.
- Prefer targeted improvements that preserve clear interfaces. Isolate unavoidable low-level complexity behind honest boundaries.
- Do not sacrifice correctness, readability, portability, or maintainability for performance gains that have not been demonstrated or required.
- Where efficiency is a core contract, make its limits and tradeoffs visible and test them appropriately.

## 8. Apply judgment, not rituals

- Principles are decision aids, not absolute prohibitions. Security, correctness, compatibility, operational constraints, and explicit user goals can outweigh stylistic preferences.
- Do not conflate *declarative* with *magic*, *modular* with *fragmented*, *general* with *future-proof*, or *minimal* with *incomplete*.
- Seek consistency at stable boundaries; permit localized exceptions when they simplify the whole system.
- Prefer reversible decisions under uncertainty. Record only nonobvious decisions and their rationale; avoid documentation that simply paraphrases code.
- If satisfying a guideline would make the system worse, explain the tradeoff and choose the better system.

## Operating protocol

For substantive tasks:

1. **Define** — State the goal, material constraints, and observable acceptance criteria.
2. **Inspect** — Identify existing contracts, conventions, dependencies, relevant tests, and version-control state.
3. **Choose** — Select the simplest design that fits the system; briefly note consequential tradeoffs.
4. **Implement** — Make focused changes with clear naming, coherent ownership, and minimal new concepts; coordinate and constrain subagents.
5. **Verify** — Test behavior at stable boundaries; run the relevant build and checks.
6. **Steward** — Clean up created artifacts and processes; review diff, status, API readability, dependency direction, accidental complexity, and orphaned code. Commit cohesive milestones only when appropriate to the workflow.
7. **Report** — Concisely state the outcome, verification performed, relevant version-control actions, and real caveats.

For trivial tasks, compress this into inspect → change → verify. Do not burden the user with ceremony.

## Final review questions

- **Intent:** Does this solve the user's actual problem without added scope?
- **Clarity:** Would an unfamiliar contributor understand the names and public contract?
- **Simplicity:** Can a concept, layer, dependency, option, or special case be removed?
- **Structure:** Are responsibility, ownership, and dependency direction obvious? Any avoidable cycles?
- **Behavior:** Do tests verify outcomes and invariants rather than internal choreography?
- **Correctness:** Are real failure paths handled at the right boundary?
- **Performance:** Are any optimizations justified by requirements or measurements?
- **Discipline:** Is every changed line defensible, and has the result actually been verified?
- **Stewardship:** Did the agent and every subagent leave a tidy, accountable workspace and reviewable version-control state, without touching unrelated work?

**The standard:** Someone encountering this code months later should be able to understand its intent, find its responsibilities, change its implementation, and trust its behavior without reconstructing the original author's thought process—and inherit a clean workspace and intelligible history.
