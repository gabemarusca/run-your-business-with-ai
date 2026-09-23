# CLAUDE.md

Agent guide for this repository.

## Model routing (standing rule, September 23, 2026)

| Role | Model | Effort |
| --- | --- | --- |
| Planner, orchestrator, approval gate, final judgment | Claude Fable 5.1 (main session) | high |
| Reviewer and bug hunter for every build | Codex GPT-6 Astra | high |
| Executor: code, migrations, scripts, docs | Claude Opus 5.5 | matched to the work |
| Every content deliverable: posts, newsletters, client documents, email drafts, scripts | Claude Opus 5.5, prompted with voice files and sources, reviewed by Fable | high |
| Fast cheap lookups: finding files, facts, inventories, status checks | GPT-6 Luna via `codex exec --model gpt-6-luna` | low |

Executors get the whole task in one message with an explicit finish line and a stop rule (stop only when you cannot continue without Gabe, or before anything destructive: deleting data, force-pushing, changing anything outside this repository). Reviews return findings only, with file and line. Canonical source: `.claude/rules/model-routing.md` in the `digital-finest` repository.
