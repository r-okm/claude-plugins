# claude-plugins

Personal Claude plugin marketplace. Skills here are meant to work on every
surface signed in to a claude.ai account: chat, Cowork, and Claude Code.

Machine-specific skills (WSL, tmux, chezmoi helpers) stay in
[dotfiles](https://github.com/r-okm/dotfiles) under `src/dot_claude/skills/`.
Cowork never reads `~/.claude/skills/`, so anything that must reach Cowork
lives here instead.

## Layout

```
.claude-plugin/marketplace.json   marketplace catalog (must stay at the repo root)
plugins/r-okm/                    the single plugin; skills are invoked as /r-okm:<skill>
  .claude-plugin/plugin.json
  skills/<skill>/SKILL.md
```

## Subscribe from a claude.ai account

Once per account (work and personal alike):

1. Customize > Plugins > Add > **Add marketplace**, enter `r-okm/claude-plugins`.
2. Install the `r-okm` plugin.
3. In the marketplace's `...` menu, turn on **Sync automatically**.

The plugin is saved to the account, so Cowork and Claude Code pick it up
without any further install. Claude Code lists it as `r-okm@synced`.

To use it in Claude Code without a claude.ai account (API key, Bedrock), install
it directly instead. This copy stays on that machine only:

```
/plugin install r-okm --marketplace r-okm/claude-plugins
```

## Release a change

Edit the skill, run `claude plugin validate .`, commit, push. Neither
`plugin.json` nor the marketplace entry sets `version`, so every commit is a
release: Claude Code takes the plugin directory's commit SHA as its version.
`claude plugin validate` warns that `plugin.json` has no `version`; that is
expected.

On claude.ai, "Sync automatically" is known not to fire on push for personal
marketplaces
([anthropics/claude-code#93825](https://github.com/anthropics/claude-code/issues/93825)).
Select **Check for updates** on the marketplace after pushing.
