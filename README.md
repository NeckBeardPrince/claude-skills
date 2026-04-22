# claude-skills

Personal Claude Code skills, packaged as a plugin marketplace.

## Install

```shell
/plugin marketplace add NeckBeardPrince/claude-skills
/plugin install adam-skills@adam-skills
```

Then reload:

```shell
/reload-plugins
```

## What's included

| Plugin        | Skills    | Description                                          |
| :------------ | :-------- | :--------------------------------------------------- |
| `adam-skills` | `hello`   | Smoke-test skill. Confirms the plugin loaded.        |

Invoke a skill with `/<plugin>:<skill>`, e.g. `/adam-skills:hello`.

## Repo layout

```
.
├── .claude-plugin/
│   └── marketplace.json          # catalog consumed by /plugin marketplace add
└── plugins/
    └── adam-skills/
        ├── .claude-plugin/
        │   └── plugin.json       # plugin manifest (name, version, author)
        └── skills/
            └── <skill-name>/
                └── SKILL.md      # one per skill
```

## Adding a new skill

1. `mkdir plugins/adam-skills/skills/<new-skill>`
2. Create `SKILL.md` with YAML frontmatter:
   ```markdown
   ---
   description: One sentence describing when Claude should invoke this.
   ---

   Instructions for Claude...
   ```
3. Commit, push, and run `/plugin marketplace update` in any session that has this marketplace added.

## Adding a new plugin

1. `mkdir -p plugins/<new-plugin>/.claude-plugin plugins/<new-plugin>/skills`
2. Add `plugins/<new-plugin>/.claude-plugin/plugin.json`
3. Add an entry to `plugins` in `.claude-plugin/marketplace.json`:
   ```json
   { "name": "<new-plugin>", "source": "<new-plugin>", "description": "..." }
   ```
   (`source` is bare because `metadata.pluginRoot` is set to `./plugins`.)

## Local development

Test without installing:

```shell
claude --plugin-dir ./plugins/adam-skills
```

Reload after edits:

```shell
/reload-plugins
```

## Versioning

Bump `version` in both `marketplace.json` (`metadata.version`) and each affected `plugin.json` when cutting a release. Tag the commit (`git tag v0.2.0 && git push --tags`) so users can pin with:

```json
{ "ref": "v0.2.0" }
```

## License

MIT — see [LICENSE](./LICENSE).
