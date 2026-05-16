# AI tooling strategy

This repository uses AI agents to help build `bmemb`, a publicly
distributed Unity UPM asset library for rhythm game development.

## Canonical guidance

- [.github/copilot-instructions.md](../.github/copilot-instructions.md)
  is the canonical, fully detailed AI guide. Keep it complete enough
  for GitHub Copilot CLI and VS Code Copilot Chat.
- [AGENTS.md](../AGENTS.md) is a Codex compatibility entry point. It
  must stay self-contained for the rules that Codex needs immediately,
  then point to the canonical Copilot guide for the remaining detail.
- [CLAUDE.md](../CLAUDE.md) is a Claude Code compatibility entry point
  with the same role.
- [GEMINI.md](../GEMINI.md) is a Gemini CLI compatibility entry point
  with the same role.

## Project-specific emphasis

- Public package quality matters more than fast one-off hacks.
- Pure rhythm-game domain logic should stay testable outside Unity scene
  setup where possible.
- Package layout, samples, docs, and release metadata should evolve
  together.
- AI agents should ask before silently choosing package identity,
  namespace roots, Unity support baselines, or breaking API changes.

## Change policy

- Prefer preserving existing Copilot behavior over abstracting too
  early.
- Duplicate only the minimum guidance needed for non-Copilot agents to
  act safely and predictably.
- Extract shared text into a neutral document only after benchmarks
  show that the Copilot-first workflow does not regress.
- When a rule uses a Copilot-specific feature name, document the
  underlying intent so other agents can map it to their own interaction
  model.

## Maintenance notes

- Treat this file as a human-facing strategy note, not as the primary
  instruction file for any agent.
- When updating AI guidance, review `README.md`,
  `.github/copilot-instructions.md`, `AGENTS.md`, `CLAUDE.md`, and
  `GEMINI.md` together.
- If the project scope expands beyond a Unity UPM rhythm-game library,
  refresh these documents before adding major new automation.
