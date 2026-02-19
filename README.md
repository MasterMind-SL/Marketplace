# MasterMind-SL Marketplace

Claude Code plugin marketplace by MasterMind-SL.

## Available Plugins

| Plugin | Description | Version |
|--------|-------------|---------|
| **[upwork-scraper](https://github.com/MasterMind-SL/Upwork-Plugin-Claude)** | Scrape Upwork jobs, analyze market demand, write proposals, optimize rates, and build portfolios. 5 slash commands + 5 AI agents. | 0.2.0 |
| **[the-council](https://github.com/MasterMind-SL/the-council-plugin)** | Adversarial consultation with persistent memory. 4 auto-routed modes, configurable roles, native agent teams. | 3.0.0 |
| **[the-council-beta](https://github.com/MasterMind-SL/the-council-plugin/tree/QA)** | BETA: All v3.0.0 features + `/council:build` — full build pipeline (PRD, tech deck, backlog) + parallel implementation. | 3.1.0-beta |

## Installation

### 1. Add the marketplace

Inside Claude Code:

```
/plugin marketplace add MasterMind-SL/Marketplace
```

### 2. Install a plugin

```
/plugin install upwork-scraper@mastermind-marketplace
/plugin install the-council@mastermind-marketplace          # stable
/plugin install the-council-beta@mastermind-marketplace     # beta (QA branch)
```

### 3. Restart Claude Code

Close and reopen Claude Code for the MCP server to connect.

### 4. Run setup

Each plugin has a setup command:

```
/upwork-scraper:setup
/council:setup
```

## Commands

Once installed, use these slash commands:

### Upwork Scraper

| Command | Description |
|---------|-------------|
| `/upwork-scraper:setup` | Install dependencies |
| `/upwork-scraper:best-matches` | Fetch personalized Best Matches |
| `/upwork-scraper:search <query>` | Search jobs with filters |
| `/upwork-scraper:analyze <skill>` | Analyze market demand |
| `/upwork-scraper:portfolio <skills>` | Get portfolio project ideas |

### The Council (stable: v3.0.0)

| Command | Description |
|---------|-------------|
| `/council:setup` | Install dependencies |
| `/council:init` | Initialize `.council/` in your project |
| `/council:consult <goal>` | Adversarial consultation (auto-routed: default, debate, plan, reflect) |
| `/council:status` | View decisions, memory health, compaction recommendations |
| `/council:maintain` | Compact memory using the curator agent |
| `/council:update` | Migrate council data after a plugin update |
| `/council:reset` | Clear session data (add `--all` to also clear memory) |

### The Council Beta (v3.1.0-beta)

All stable commands above, plus:

| Command | Description |
|---------|-------------|
| `/council:build <goal>` | Full build pipeline: 3 consultations (PRD, tech deck, backlog) + parallel implementation with dev teams |

> **Note**: Beta installs from the QA branch. Expect changes. Token-intensive (~50k-150k+ tokens per build).

## Updating

```
/plugin marketplace update mastermind-marketplace
```

## List available plugins

```
/plugin marketplace list mastermind-marketplace
```

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) v1.0.33+
- Agent teams enabled: `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`
- Python 3.11+
- [uv](https://docs.astral.sh/uv/)

## License

MIT
