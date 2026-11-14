# CLAUDE.md

Agent guide for this repository.

## Model routing

Gabe's rule since November 13, 2026: Opus 5.5 does general work and Fable 5.2 does complex work; Codex GPT-6 Astra reviews Fable 5.2, and Fable 5.2 and Codex GPT-6 Astra review Opus 5.5.

| Role | Model | Effort |
| --- | --- | --- |
| General work and the default main session: everyday engineering, debugging, bug fixes, scripts, doc edits, content drafts of any length, research synthesis, and anything not clearly complex | Claude Opus 5.5 (`model: "opus"`) | medium, then high |
| Complex work: major refactors and migrations, architecture planning, deep research, hard judgment calls | Claude Fable 5.2 | medium, then high |
| Review of Opus 5.5 work | Claude Fable 5.2 and Codex GPT-6 Astra | high |
| Review of Fable 5.2 work | Codex GPT-6 Astra | high |
| Lookups and side tasks: finding files, reading logs, inventories, extraction | Claude Haiku 5.5 (`model: "haiku"`) in Claude Code; GPT-6 Luna via `codex exec --model gpt-6-luna` from Codex and df-run | the model's default |

Sonnet 5.5 is no longer a default role. When Opus 5.5 at high falls short, hand the task to Fable 5.2. Delegate only when a bounded, independent unit is worth a subagent's context overhead; a small edit or a short lookup stays in the main session. Executors get the whole task in one message with an explicit finish line and a stop rule (stop only when you cannot continue without Gabe, or before anything destructive: deleting data, force-pushing, changing anything outside this repository). Reviews return findings only, with file and line. Canonical source: `.claude/rules/model-routing.md` in the `digital-finest` repository; where the two differ, the canonical file wins.
