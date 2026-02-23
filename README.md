# MasterMind-SL Marketplace

Claude Code plugin marketplace by MasterMind-SL.

## Available Plugins

| Plugin | Description | Version |
|--------|-------------|---------|
| **[upwork-scraper](https://github.com/MasterMind-SL/Upwork-Plugin-Claude)** | Scrape Upwork jobs, analyze market demand, write proposals, optimize rates, and build portfolios. 5 slash commands + 5 AI agents. | 0.2.0 |
| **[the-council](https://github.com/MasterMind-SL/the-council-plugin)** | Adversarial consultation with persistent memory. 4 auto-routed modes, configurable roles, `/council:build` pipeline, anti-deferral system, intelligent memory retrieval. | 3.1.0 |

## Installation

### 1. Add the marketplace

Inside Claude Code:

```
/plugin marketplace add MasterMind-SL/Marketplace
```

### 2. Install a plugin

```
/plugin install upwork-scraper@mastermind-marketplace
/plugin install the-council@mastermind-marketplace
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

### The Council (v3.1.0)

| Command | Description |
|---------|-------------|
| `/council:setup` | Install dependencies |
| `/council:init` | Initialize `.council/` in your project |
| `/council:consult <goal>` | Adversarial consultation (auto-routed: default, debate, plan, reflect) |
| `/council:build <goal>` | Full build pipeline: 3 consultations (PRD, tech deck, backlog) + feature completeness gate + implementation |
| `/council:status` | View decisions, memory health, compaction recommendations |
| `/council:maintain` | Compact memory using the curator agent |
| `/council:update` | Migrate council data after a plugin update |
| `/council:reset` | Clear session data (add `--all` to also clear memory) |

**What's new in v3.1.0:**
- **`/council:build` pipeline** — 3 consultations (PRD, tech deck, backlog) + feature completeness gate + implementation with 1 dev team (3-4 members, each with subagent parallelization).
- **Anti-deferral system** — Agents never cut, defer, or deprioritize features. Everything the user asks for gets implemented.
- **Quality Engineer critic** — Improves quality (security, architecture, error handling) instead of managing scope.
- **Claude Velocity** — All agents understand Claude Code implements in ~2 hours, not weeks.
- **Unified banned words** — All 5 agents share the same complete banned words list (P0/P1/P2, scope creep, defer, etc.).
- **Synonym expansion** — Topic matching works across 50+ synonym pairs (e.g. "autoscaling" → "performance", "postgres" → "database") plus bigrams.
- **Staleness markers** — Memory entries older than 90 days show `[stale: Xd]` and score 0.7× in relevance. Pinned entries always exempt.
- **3-tier memory packing** — Detail adapts to token budget: full text when generous, smart upgrade pass when normal, one-liners when tight.
- **Archive top-12 by relevance** — Archive excerpts select the most relevant lessons (was last-5 by recency).
- **MEMORY LENS directives** — Each teammate receives a role-specific lens before the injected memory block.

> **After updating**: Run `/council:update` in each project with `.council/` to migrate data.

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
