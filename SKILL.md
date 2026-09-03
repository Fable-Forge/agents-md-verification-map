---
name: agents-md-verification-map
description: Use when auditing, creating, or tightening a project AGENTS.md verification map with concrete T0-T3 checks, repo-specific commands, anti-weakening rules, pending_external boundaries, or global-vs-project instruction compression.
---

# AGENTS.md Verification Map

## Overview

Write short, project-specific `AGENTS.md` guidance that maps change risk to real validation commands. Keep global rules compact; put checkout-specific commands, source-of-truth paths, and acceptance boundaries in the project file.

## Workflow

1. Confirm target and authority.
   - Identify the exact repo root and the `AGENTS.md` file to edit.
   - Respect nested repo boundaries. If the user names a nested root, keep parent files read-only unless explicitly allowed.
   - Preserve existing dirty or untracked work. Do not reset, stash, reformat, or widen the write set.

2. Audit real verification surfaces before writing.
   - Read `package.json`, test folders, tool scripts, docs, project files, and existing QA notes only as needed.
   - Use only commands and files that actually exist.
   - For Godot/Cocos projects, distinguish static contracts, headless/import checks, editor preview, real-window/device checks, and external human review.
   - For web projects, distinguish typecheck/lint/unit tests, build, browser/E2E, local simulation, real integration, and deployment.

3. Write the smallest useful map.
   - T0: doc/copy/config-only changes use repo-wide `git diff --check` plus manual current Diff inspection.
   - T1: nearest focused test, static check, or targeted validator.
   - T2: fuller automated build, contract, smoke, headless, or E2E coverage for new behavior or cross-file changes.
   - T3: release, payment, auth, safety, permissions, real platform, device, real-window, or external-human validation. Keep this separate from automation and mark unavailable evidence as `pending_external`.
   - Add one project-specific anti-weakening rule: do not delete, skip, loosen, fake, bypass, or relabel tests and acceptance gates to make an implementation pass.

4. Avoid weak long-lived wording.
   - Do not use placeholders such as `<相关测试>` or vague lines like “run relevant checks”.
   - Do not invent scripts, paths, scenes, devices, credentials, services, or QA proof.
   - Do not make every edit run the full suite; map validation to risk.
   - Do not claim local simulation is real external integration.

5. Verify the policy edit.
   - Re-read the edited block.
   - Run `git diff --check` at repo scope for T0 hygiene.
   - If the file is untracked, manually inspect the full file because `git diff` may not show it.
   - Confirm the diff touches only the intended `AGENTS.md` unless broader writes were explicitly authorized.

## Output Contract

Report the target file, evidence inspected, inserted or changed T0-T3 map, verification actually run, unverified T3/external gates, and any scope deliberately left untouched.
