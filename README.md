# MasterMind-SL Marketplace

Claude Code plugin marketplace by MasterMind-SL.

## Available Plugins

| Plugin | Description | Version |
|--------|-------------|---------|
| **[upwork-scraper](https://github.com/MasterMind-SL/Upwork-Plugin-Claude)** | Scrape Upwork jobs, analyze market demand, write proposals, optimize rates, and build portfolios. 5 slash commands + 5 AI agents. | 0.2.0 |
| **[the-council](https://github.com/MasterMind-SL/the-council-plugin)** | Adversarial consultation with persistent memory. 4 auto-routed modes, configurable roles, `/council:build` pipeline, anti-deferral system, intelligent memory retrieval. | 3.1.0 |
| **[computer-vision](https://github.com/MasterMind-SL/computer-vision-plugin)** | Desktop computer vision and input control for Windows. 17 tools: screenshots, click, type, scroll, OCR, natural language element finder (`cv_find`), text extraction (`cv_get_text`), UI trees. Atomic keyboard with hwnd, post-action screenshots, vision-enhanced find. Like Claude-in-Chrome, but for any app. | 1.6.0 |

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
/plugin install computer-vision@mastermind-marketplace
```

### 3. Restart Claude Code

Close and reopen Claude Code for the MCP server to connect.

### 4. Run setup

Each plugin has a setup command:

```
/upwork-scraper:setup
/council:setup
/cv-setup
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

### Computer Vision (v1.6.0)

**What's new in v1.6.0:**
- **Atomic keyboard with hwnd** — `cv_type_text` and `cv_send_keys` accept optional `hwnd` parameter for atomic focus+type+verify in a single tool call. 3-retry loop with TOCTOU mitigation. Type into Chrome's address bar without losing focus to the terminal.
- **Post-action screenshots** — Every mutating tool (`cv_type_text`, `cv_send_keys`, `cv_mouse_click`, `cv_scroll`) returns `image_path` with a screenshot taken after the action. Enables see-act-verify loop. Opt-out with `screenshot=False`.
- **cv_scroll** — New dedicated scroll tool. Scroll any window in any direction (up/down/left/right) with configurable amount. Supports window-relative coordinates for targeted scrolling.
- **Vision-enhanced cv_find** — Success responses always include a screenshot with `image_scale` and `window_origin` metadata, enabling Claude to visually verify matches and compute click coordinates from the downscaled image.
- **Window state metadata** — Every tool with `hwnd` returns `window_state` (title, is_foreground, rect) for state awareness between tool calls.

**v1.5.0:** Robust 4-strategy window focus, PrintWindow-first capture, Chrome/Electron accessibility, vision fallback on no-match, GDI leak fix.
**v1.4.0:** `cv_find`, `cv_get_text`, OCR bounding boxes, security hardening.
**v1.3.0:** File-based screenshots, auto-cleanup.
**v1.2.0:** OCR optimization via `capture_region_raw()`.

| Tool | Description |
|------|-------------|
| `cv_list_windows` | List all visible windows with HWND, title, process, rect |
| `cv_screenshot_window` | Capture a window — returns `image_path` for native viewing |
| `cv_screenshot_desktop` | Capture the desktop — returns `image_path` for native viewing |
| `cv_screenshot_region` | Capture a region — returns `image_path` for native viewing |
| `cv_focus_window` | Bring a window to the foreground |
| `cv_mouse_click` | Click at screen coordinates (left/right/double/middle/drag) — returns screenshot |
| `cv_type_text` | Type text with optional `hwnd` for atomic focus+type — returns screenshot |
| `cv_send_keys` | Send key combinations with optional `hwnd` for atomic focus+send — returns screenshot |
| `cv_scroll` | Scroll a window (up/down/left/right) with configurable amount — returns screenshot |
| `cv_move_window` | Move/resize a window or maximize/minimize/restore |
| `cv_ocr` | Extract text with word-level bounding boxes and confidence |
| `cv_find` | Find elements by natural language (UIA + OCR fuzzy search) |
| `cv_get_text` | Extract all visible text (UIA primary, OCR fallback) |
| `cv_list_monitors` | List all monitors with resolution, DPI, and position |
| `cv_read_ui` | Read the UI accessibility tree of a window |
| `cv_wait_for_window` | Wait for a window matching a title pattern to appear |
| `cv_wait` | Simple delay (max 30 seconds) |

| Command | Description |
|---------|-------------|
| `/cv-setup` | Verify setup and dependencies |
| `/cv-help` | Usage guide and examples |

> **Requirements:** Windows 10 21H2+ or Windows 11, Python 3.11+, [uv](https://docs.astral.sh/uv/)

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
