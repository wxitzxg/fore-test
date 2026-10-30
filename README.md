# fore-test

Test repo for the [`fore`](https://github.com/wxitzxg/fore) skills library. It's a sandbox for exercising `fore` against a real repository — publishing specs, turning them into tickets, and running the agent conventions those skills depend on — not a product.

## Relationship to `fore`

`fore-test` consumes `fore`; it doesn't own or vendor it. Each entry under [`.claude/skills/`](.claude/skills/) is a **symlink** into a local checkout of `fore`, mirroring its `skills/<category>/<name>` layout. For example:

```
.claude/skills/to-spec     ->  <fore checkout>/skills/engineering/to-spec
.claude/skills/grilling    ->  <fore checkout>/skills/productivity/grilling
```

The categories present (`engineering/`, `productivity/`) reflect whichever skills `fore` has wired in; the skills themselves stay in the `fore` repo.

## Repo layout

| Path              | What it is                                                              |
| ----------------- | ----------------------------------------------------------------------- |
| `README.md`       | This file                                                                |
| `CLAUDE.md`       | Project instructions for the Claude Code CLI                             |
| `docs/agents/`    | The three agent contracts that make the skills runnable here             |
| `.claude/skills/` | Symlinks into the `fore` skills library                                  |
| `hello.txt`       | Placeholder                                                              |

## Agent contracts

The skills operate on three contracts, each one file under [`docs/agents/`](docs/agents/):

- [`issue-tracker.md`](docs/agents/issue-tracker.md) — where issues and specs live (GitHub, driven through `gh`).
- [`triage-labels.md`](docs/agents/triage-labels.md) — the triage role vocabulary.
- [`domain.md`](docs/agents/domain.md) — how domain docs (`GLOSSARY.md`, `docs/adr/`) are consumed.

## Running a skill

In the Claude Code CLI, type `/<skill-name>` to invoke a skill — for example `/to-spec` to publish a spec, or `/to-tickets` to break it into tickets.

## Triage labels

Five canonical triage roles, plus one separate container label:

| Role           | Meaning                                    |
| -------------- | ------------------------------------------ |
| `needs-triage` | Needs maintainer evaluation                |
| `needs-info`   | Waiting on reporter for more information   |
| `ready-for-agent` | Fully specified, ready for an AFK agent |
| `ready-for-human` | Requires human implementation           |
| `wontfix`      | Will not be actioned                       |

The `spec` label is separate from the triage roles: it marks a spec issue published by `/to-spec`, the container its tickets hang under. Only spec issues carry it — task tickets never do.