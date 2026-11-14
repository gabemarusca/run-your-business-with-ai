# CLAUDE.md

Agent guide for this repository.

## Model routing

| Role | Model | Effort |
| --- | --- | --- |
| Planner, orchestrator, approval gate, final judgment; major refactors, migrations and architecture | Claude Fable 5.2 (main session) | medium, then high |
| Reviewer and bug hunter for every build | Codex GPT-6 Astra | high |
| Executor for multi-file builds, debugging, harder migrations, and anything not clearly scoped | Claude Opus 5.5 (`model: "opus"`) | medium, then high |
| Executor for well-scoped work: a bug fix, a feature built against a written spec, a small script or doc edit | Claude Sonnet 5.5 (`model: "sonnet"`) | medium, then high |
| Content built from large sources or long in a voice: newsletters, client documents, scripts | Claude Opus 5.5, prompted with voice files and sources, reviewed by Fable | high |
| Everyday short drafts: email and message replies, single posts, captions | Claude Sonnet 5.5, same brief, reviewed by Fable | high |
| Fast cheap lookups: finding files, reading logs, facts, inventories, status checks | Claude Haiku 5.5 (`model: "haiku"`) in Claude Code; GPT-6 Luna via `codex exec --model gpt-6-luna` from Codex | the model's default |

Delegate only when a bounded, independent unit is worth a subagent's context overhead; a small edit or a short lookup stays in the main session. Executors get the whole task in one message with an explicit finish line and a stop rule (stop only when you cannot continue without Gabe, or before anything destructive: deleting data, force-pushing, changing anything outside this repository). Reviews return findings only, with file and line. Canonical source: `.claude/rules/model-routing.md` in the `digital-finest` repository; where the two differ, the canonical file wins.
