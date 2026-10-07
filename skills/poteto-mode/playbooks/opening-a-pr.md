### Opening a PR

Invoked at the end of every other playbook.

**The user's rules come first.** Read the user's global and project instruction files (`CLAUDE.md`, `AGENTS.md`) before the first branch, commit, or PR operation. Follow them for branches, worktrees, commits, review steps, PR titles, PR descriptions, and writing style. They replace this playbook on each of those points. Where they say nothing, use the sections below. Never mix a convention from here into a PR that the user's rules already cover.

**Forge.** Resolve the forge before the first PR operation and keep that choice for create, edit, view, watch, and merge. GitHub CLI (`gh`) is the default. If `command -v origin` succeeds and Origin can resolve the repository, prefer `origin pr ...`. If Origin is absent or cannot resolve the repository, stay on `gh` and record the fallback. Do not require Graphite (`gt`).

**Review.** Run `/no-comments` over the diff before the PR goes up, after the review steps the user's rules name. It adds to those steps and is not replaced by them.

**Size and stacks.** Prefer five narrow PRs to one large PR. A stack is a base-branch chain. The root PR targets the base branch the user's rules name, or trunk when they name none. Each child branch rebases onto its parent's exact tip and its PR targets the parent branch. Create a child with `origin pr create --status open --base <parent-branch>` or `gh pr create --base <parent-branch>` according to the resolved forge. Retarget an existing child with `origin pr edit <pr> --base <parent-branch>` or `gh pr edit <pr> --base <parent-branch>`. Branch from the base branch only for independent work. Rebase on it before substantial stack work.

**Readiness.** Open every PR ready, never as a draft. With Origin, pass `--status open`. With `gh`, omit `--draft`. Cloud-agent PR tools default to draft, so set `draft: false` on every PR creation call. If a PR still opens as a draft, run `origin pr ready <number>` or `gh pr ready <number>` according to the resolved forge. Run `origin pr view <number>` or `gh pr view <number>` before you refer to PR status. In T3 Code, call `link_pull_request` with the URL of every PR you open or retarget (see **Harness** in SKILL.md).

**Babysit.** Opening a PR does not start a babysit. Post the URL and keep building. Finish the phase or stack first. Run a separate babysit pass only when the user asks for one after the whole stack exists. A babysit for each new PR stalls the build and spends checks on commits that later waves restart. Push back when feedback drifts from intent.

A subagent that opens a PR runs `interrogate`, the review steps the user's rules name, and `/no-comments`. It returns the URL and does not babysit. Return to the parent.
