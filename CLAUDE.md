# MasterMind-SL Marketplace — Maintainer Instructions

## Structure

This is the central plugin registry for MasterMind-SL. Each plugin lives in its own repo:

| Plugin | Repo | Current Version |
|--------|------|-----------------|
| upwork-scraper | `MasterMind-SL/Upwork-Plugin-Claude` | 0.2.0 |
| the-council | `MasterMind-SL/the-council-plugin` (main) | 3.1.0 |
| computer-vision | `MasterMind-SL/computer-vision-plugin` | 1.3.0 |

## When Publishing a New Plugin Version

1. Make and push changes in the plugin repo
2. Update `.claude-plugin/marketplace.json` here: bump the version and description for the plugin
3. Update `README.md` here: bump the version in the table and update commands if changed
4. Commit and push this repo

## When Publishing a Beta Version

1. Push feature branch (e.g., QA) to the plugin repo
2. Add a new entry to `marketplace.json` with `"ref": "branch-name"` in the source object
3. Use a versioned name like `plugin-name-beta` to keep it separate from stable
4. Update README with beta section and commands
5. When beta is promoted to stable: merge branch to main, update the stable entry version, remove the beta entry

## When Adding a New Plugin

1. Create the plugin repo with `.claude-plugin/plugin.json` and `.mcp.json`
2. Add a new entry to the `plugins` array in `.claude-plugin/marketplace.json`
3. Add the plugin to the README table and commands section
4. Commit and push

## Installation Flow (for users)

```
/plugin marketplace add MasterMind-SL/Marketplace
/plugin install <plugin-name>@mastermind-marketplace
```

## Files

- `.claude-plugin/marketplace.json` — Plugin registry (source of truth for available plugins and versions)
- `README.md` — Public documentation for users
