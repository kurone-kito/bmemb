# Guidelines for AI Agents

This repository hosts `bmemb`, a Unity UPM asset library for rhythm
game development intended for public distribution.

When contributing to this repository using AI agents, follow these
guidelines to keep the package reusable, reviewable, and friendly to
downstream Unity projects.

## Tooling priority and compatibility

This repository is intentionally optimized for GitHub Copilot CLI and
VS Code Copilot Chat because they are the primary tools used for
day-to-day work and benchmarking.

`AGENTS.md`, `CLAUDE.md`, and `GEMINI.md` exist as lightweight
compatibility entry points for Codex, Claude Code, and Gemini CLI
respectively. Keep this file as the canonical, fully detailed guide
unless benchmark results justify a more neutral layout.

## Conversation

- Match the conversational language to the user's language.
- Write comments, code documentation, and repository-facing prose in
  English unless the surrounding file clearly uses another language.
- Continue autonomously for low-risk work, but pause and ask a concise
  question when the next step would silently lock in package identity,
  public API shape, Unity version support, serialization format, or
  release/distribution behavior.
- When a pause is needed, provide recommended options instead of an
  open-ended prompt.

## Project profile

- Build a reusable Unity package for rhythm game systems and tooling.
- Optimize for public consumption by Unity developers rather than a
  single game's private scene hierarchy.
- Favor a small dependency surface, clear installation steps, and
  predictable upgrade behavior.
- Treat this repository as a package product first: code, samples,
  documentation, and release metadata should move together.

## Package layout and distribution

When creating package content, prefer a standard UPM structure:

- `package.json`
- `Runtime/`
- `Editor/`
- `Tests/`
- `Samples~/`
- `Documentation~/`
- `CHANGELOG.md`
- `LICENSE.md`
- one or more `.asmdef` files

Additional rules:

- Keep distributable code and assets inside the package boundary.
- Keep runtime and editor code in separate assemblies.
- Do not rely on project-local `Assets/` content unless it is shipped as
  a sample or part of an explicitly documented development harness.
- Avoid introducing generated Unity folders such as `Library/`, `Temp/`,
  or `Obj/`.
- Avoid large binary assets unless they are required for the package and
  explicitly approved.
- If the repository layout has not been finalized yet, do not silently
  invent the final package name, assembly names, or namespace root.
  Confirm them first, then apply them consistently.

## Architecture preferences

- Separate pure domain logic from Unity-facing adapters whenever
  possible. Timing rules, chart data, judgement, and scoring logic
  should be testable without scene setup.
- Make time sources explicit. Document whether a system depends on DSP
  time, game time, unscaled time, or a custom clock abstraction.
- Design extension points for multiple rule sets, note types, or chart
  formats instead of encoding one game's assumptions into the public API.
- Keep editor tooling optional and isolated under `Editor/`.
- Prefer composition and narrow interfaces over hard-wired singletons or
  hidden global state.

## Testing strategy

- Use Unity Test Framework as the default testing approach.
- Prefer edit mode tests for pure logic and play mode tests only when
  engine behavior genuinely matters.
- Add focused regression tests for public API behavior,
  serialization-sensitive code, and timing-related edge cases.
- Keep fixtures small and text-based where practical so they are easy to
  review.
- If Unity version-specific behavior matters, document the tested
  version in the related change or test notes.

## Coding standards

- Follow the repository's current formatting baseline:
  - 2-space indentation
  - LF line endings
  - trimmed trailing whitespace except in Markdown
  - final newline always present
  - lowercase-with-hyphens file names unless a platform convention
    requires something else
- Keep comments short and explanatory. Prefer naming and structure over
  narration.
- Minimize `.meta` churn. When Unity assets or folders are introduced,
  commit the matching `.meta` files intentionally.
- Do not modify community documents (`CODE_OF_CONDUCT*`,
  `CONTRIBUTING*`) without explicit approval.

## Release and versioning expectations

- Treat the package as a semver-managed public artifact.
- Keep package metadata, samples, and docs aligned with the shipped API.
- Call out breaking API or behavior changes clearly in changelog and
  upgrade notes.
- Prefer additive, backwards-compatible changes unless the user has
  explicitly approved a breaking revision.

## Branch strategy

This project follows
[GitHub Flow](https://docs.github.com/en/get-started/using-git/github-flow):
`main` is the only long-lived branch and every change reaches `main`
through a pull request.

### Rules

- **Never push directly to `main`** — all changes must go through a
  pull request. Branch protection is enforced on GitHub.
- **Rebase onto `main`** — when a feature branch needs the latest
  `main`, always rebase. Fetch first so the local `main` is not stale,
  for example `git fetch origin && git rebase origin/main`. Do not
  create merge commits inside feature branches.
- **Rebase between feature branches** — if one feature branch needs
  changes from another, use rebase, not merge.
- **Merge commits at PR boundary** — pull requests into `main` are
  merged with a merge commit.
- **fixup + autosquash for in-branch fixes** — when a later commit in a
  feature branch fixes an earlier one, prefer
  `git commit --fixup=<sha>` followed by
  `git rebase -i --autosquash`.
- **Avoid giant commits** — if squashing would produce an unreasonably
  large commit, keep the fix commit separate or re-split the history so
  each commit remains reviewable.

## Commit rules

This project follows
[Conventional Commits](https://www.conventionalcommits.org/).
A `.gitmessage` template is available at the repository root for
guidance when writing commit messages. Contributors who want the
template prefilled in their editor should opt in once per clone:

```sh
git config commit.template .gitmessage
```

### Format

```txt
<type>[optional scope]: <user-facing description>

<body: purpose, context, and what changed>

[optional footer(s)]
```

### Subject line

- Use the format: `<type>[optional scope]: <description>`
- Write from the user's perspective
- Write in lowercase, imperative mood
- Keep the subject line under 72 characters
- Do not end the subject line with a period

### Types and scopes

- Common types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`,
  `chore`, `ci`, `build`, `perf`
- Prefer short lowercase scopes such as `runtime`, `editor`, `tests`,
  `docs`, `ci`, or a package/module name once those exist

### Body and trailers

- Explain why the change exists, the relevant context, and what changed
- Wrap body lines at 72 characters
- Use trailers such as `Refs #<issue>`, `Closes #<issue>`, and
  `BREAKING CHANGE: ...` when appropriate

### Atomic commits

- Keep one logical change per commit
- Separate refactoring from behavior changes
- Separate formatting churn from functional work
- Separate dependency updates from code changes when practical
