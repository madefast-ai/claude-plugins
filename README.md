# Madefast plugins for Claude

The `madefast` plugin marketplace. It lists the plugins; each one lives in its own repository and is updated there.

| Plugin | What it does | Repository |
|---|---|---|
| `cc` | Generates and maintains a complete Claude Code setup for any project | [madefast-ai/claude-code-setup](https://github.com/madefast-ai/claude-code-setup) |
| `leads` | Lead Finder: B2B leads on LinkedIn, Reddit and Instagram, engaged in public first | [madefast-ai/lead-finder-plugin](https://github.com/madefast-ai/lead-finder-plugin) |
| `mradik` | Lets Claude Code ask other local repositories questions | [madefast-ai/mradik-plugin](https://github.com/madefast-ai/mradik-plugin) |
| `madefast-tools` | Bottom bar, tools panel and Clean View for Claude Code | [madefast-ai/madefast-tools](https://github.com/madefast-ai/madefast-tools) |

## Install

Claude Code:

```bash
claude plugin marketplace add madefast-ai/claude-plugins
claude plugin install mradik@madefast      # or cc@madefast, leads@madefast, madefast-tools@madefast
```

Claude Desktop: **Customize → Plugins → Add marketplace → Add from a repository**, enter `madefast-ai/claude-plugins`, then install the plugin you want.

## Updates

```bash
claude plugin marketplace update madefast
claude plugin update mradik@madefast
```

Then restart Claude Code. In Claude Desktop: **Customize → Plugins → Check for updates**.

## Adding a plugin

Add an entry to `.claude-plugin/marketplace.json`: `"source": { "source": "github", "repo": "<owner>/<repo>" }` when the plugin is at the repository root, or `{ "source": "git-subdir", "url": "https://github.com/<owner>/<repo>.git", "path": "<folder>" }` when it is in a folder. Versions live only in each plugin's own `.claude-plugin/plugin.json`.
