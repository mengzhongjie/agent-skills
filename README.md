# agent-skills

CLI-backed skills for AI agents. Each skill teaches an agent how to drive a CLI;
the CLI itself is installed on first use by the skill's own preflight.

## Layout

```
skills/<name>/
  SKILL.md              # frontmatter + workflow + preflight
  references/*.md       # loaded on demand, not upfront
```

## The contract

1. **Preflight comes first.** Every SKILL.md opens with a numbered preflight: probe the
   binary (`<tool> version`), install it if missing through exactly one supported path,
   and stop and report if that still fails. An agent must never silently fall back to
   a different strategy.
2. **No flag lists in the skill.** The skill points at `<tool> --help` and any bundled
   `skills get <topic>` output instead, so a CLI upgrade never drifts from the skill.
3. **Errors branch on codes, not messages.** Message text changes between versions;
   machine-readable codes do not.
4. **The binary wins.** Where bundled docs and the checked-in SKILL.md disagree, the
   installed binary's docs are authoritative.

## Skills

| skill | CLI | install |
|---|---|---|
| agent-desktop | `agent-desktop` (Rust, macOS/Windows/Linux) | `npm install -g agent-desktop` |

## Provenance

`skills/agent-desktop` is adapted from [vercel-labs/agent-desktop](https://github.com/vercel-labs/agent-desktop)
(Apache-2.0). The only structural change is the Preflight section, which the upstream
skill does not have.
