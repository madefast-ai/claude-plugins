# Madefast plugins for Claude

The `madefast` plugin marketplace. It lists the Madefast plugins; each plugin lives in its own repository and is released there.

| Plugin | What it does | Works in | Repository |
|---|---|---|---|
| `cc` | Generates and maintains a complete Claude Code setup (CLAUDE.md, rules, agents, commands, guard hook) for any project | Claude Code | [madefast-ai/claude-code-setup](https://github.com/madefast-ai/claude-code-setup) |
| `mradik` | Lets Claude Code ask other local repositories questions through a read-only agent | Claude Code | [madefast-ai/mradik-plugin](https://github.com/madefast-ai/mradik-plugin) |
| `madefast-tools` | Bottom bar, tools panel and Clean View: mradik registration, current task, fleet, backlog, agents, usage | Claude Code | [madefast-ai/madefast-tools](https://github.com/madefast-ai/madefast-tools) |

Lead Finder has its own marketplace: see [madefast-ai/lead-finder-plugin](https://github.com/madefast-ai/lead-finder-plugin#readme) (`leads@leadfinder`).

## 1. Add the marketplace (once)

**Claude Code:**

```bash
claude plugin marketplace add madefast-ai/claude-plugins
```

**Claude Desktop:** **Customize → Plugins → Add marketplace → Add from a repository**, enter `madefast-ai/claude-plugins`, click **Add**.

## 2. Install plugins

### Everything at once (Claude Code)

```bash
claude plugin install cc@madefast
claude plugin install mradik@madefast
claude plugin install madefast-tools@madefast
```

Then restart Claude Code. Inside a session, `/plugin install <name>@madefast` does the same.

### One by one

#### cc — Claude Code setup

Requires Node.js 20 or newer on `PATH`.

```bash
claude plugin install cc@madefast
```

Restart Claude Code, then inside a project run `/cc:init` (new project with a brief) or `/cc:init --existing` (existing code). Details: [claude-code-setup](https://github.com/madefast-ai/claude-code-setup#readme).

#### mradik — cross-repository questions

Requires Node.js 20 or newer, and the `claude` CLI on `PATH` (otherwise set `CLAUDE_PATH` to the output of `which claude`).

```bash
claude plugin install mradik@madefast
```

Restart Claude Code, then register your repositories: ask Claude to "register this project in mradik" in each one (`add_project`). From then on any of them can `ask_project` the others. Details: [mradik-plugin](https://github.com/madefast-ai/mradik-plugin#readme).

#### madefast-tools — tools panel

```bash
claude plugin install madefast-tools@madefast
```

Restart Claude Code. The bottom bar appears; `/mf` toggles the tools panel, `/mf backlog`, `/mf fleet`, `/mf agents`, `/mf mradik` open a view. Works best with `mradik` installed.

## Updating

**Claude Code:**

```bash
claude plugin marketplace update madefast
claude plugin update cc@madefast            # and/or mradik@madefast, madefast-tools@madefast
```

Then restart Claude Code.

**Claude Desktop:** **Customize → Plugins → Check for updates**, or automatically when sync is on.

## Uninstalling

```bash
claude plugin uninstall mradik@madefast     # one plugin
claude plugin marketplace remove madefast   # the marketplace and every plugin installed from it
```

## Switching from the old per-plugin marketplaces

Earlier, some plugins were their own marketplace. Only one marketplace can be called `madefast`, so remove the old ones first, then add this one and reinstall:

| You added | Remove it with |
|---|---|
| `madefast-ai/claude-code-setup` (as `madefast`) | `claude plugin marketplace remove madefast` |
| `madefast-ai/lead-finder-plugin` (as `madefast`) | `claude plugin marketplace remove madefast`, then add it again: it is now named `leadfinder` |
| `madefast-ai/mradik-plugin` (as `mradik`) | `claude plugin marketplace remove mradik` |

In Claude Desktop, remove the old marketplace in **Customize → Plugins**, then add `madefast-ai/claude-plugins`.

## Adding a plugin to this marketplace

Add an entry to `.claude-plugin/marketplace.json`:

- plugin at the root of its repository: `"source": { "source": "github", "repo": "<owner>/<repo>" }`
- plugin in a folder: `"source": { "source": "git-subdir", "url": "https://github.com/<owner>/<repo>.git", "path": "<folder>" }`

Versions live only in each plugin's own `.claude-plugin/plugin.json`; this repository never needs a release when a plugin is updated. Check with `claude plugin validate .` before pushing.
