# MasterMind-SL Marketplace — Maintainer Instructions

## Structure

This is the central plugin registry for MasterMind-SL. Each plugin lives in its own repo:

| Plugin | Repo | Current Version |
|--------|------|-----------------|
| upwork-scraper | `MasterMind-SL/Upwork-Plugin-Claude` | 0.2.0 |
| the-council | `MasterMind-SL/the-council-plugin` | 3.0.0 |

## When Publishing a New Plugin Version

1. Make and push changes in the plugin repo
2. Update `.claude-plugin/marketplace.json` here: bump the version and description for the plugin
3. Update `README.md` here: bump the version in the table and update commands if changed
4. Commit and push this repo

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
