# Guidelines for AI Agents

This repository hosts `bmemb`, a Unity UPM asset library for rhythm
game development intended for public distribution.
It is currently optimized for GitHub Copilot tooling, but `CLAUDE.md`
exists so Claude Code can still receive the minimum project rules
immediately, without depending on a redirect.

## Immediate rules

- Match the conversational language to the user's language.
- Write comments and documentation in English unless the surrounding
  file clearly uses another language.
- If uncertainty, hidden risk, or missing context blocks a safe change,
  stop and ask a concise question with recommended options before
  proceeding.
- Keep changes small and reviewable. If you create commits, follow the
  project's Conventional Commits rules and keep each commit atomic.
- Do not modify community documents (`CODE_OF_CONDUCT*`,
  `CONTRIBUTING*`) without explicit approval.

## Project priorities

- Treat this repository as a reusable Unity package, not as a single
  game's private project.
- Prefer a standard UPM layout such as `package.json`, `Runtime/`,
  `Editor/`, `Tests/`, `Samples~/`, and `Documentation~/`.
- Keep runtime and editor code in separate assemblies.
- Separate pure rhythm-game domain logic from Unity-facing adapters so
  timing, chart, and judgement code remains testable.
- Make time sources explicit and avoid hidden global state.
- Do not silently lock in the final package name, assembly names,
  namespace root, Unity support baseline, or serialization format
  unless they are already established in the repository.
- Treat public APIs, samples, and docs as one surface: when behavior
  changes, keep them in sync.

## Project standards

- **Indentation**: 2 spaces
- **Line endings**: LF only
- **Trailing whitespace**: trimmed except in Markdown
- **Final newline**: always present
- **File naming**: lowercase with hyphens unless a platform convention
  requires otherwise

## Commit rules

This project follows
[Conventional Commits](https://www.conventionalcommits.org/).
A `.gitmessage` template is available at the repository root.
Write user-facing, lowercase subjects, keep them under 72 characters,
and split unrelated changes into separate atomic commits.

## Branch strategy

This project follows GitHub Flow. All changes reach `main` through
pull requests, and feature branches are rebased onto `main` rather than
merged. See the full rules in
[.github/copilot-instructions.md](.github/copilot-instructions.md#branch-strategy).

## Canonical reference

The full, Copilot-first project guidance lives in
[.github/copilot-instructions.md](.github/copilot-instructions.md).
When that file uses Copilot-specific workflow names, apply the intent
in Claude Code using its own interaction model rather than following
the product terms literally.
