# Theophysics Hub — Personal Dashboard
### POF 2828 · David Lowe · Oklahoma City

---

## What This Is

A unified personal dashboard that starts as standalone HTML files on a Windows desktop and scales into a full Cloudflare-hosted PWA with AI agents that learn, organize, and build autonomously.

Built by a human and AI together. From the jump. More on that below.

---

## The System

Four standalone HTML tools → one unified hub dashboard → Cloudflare PWA with AI.

**Phase 1 — Local Tools (now):**
Single HTML files. No framework. No server. No build step. localStorage only. Double-click and go. Drop them in your Windows Startup folder and they launch on boot.

| Tool | File | Status |
|------|------|--------|
| Clipboard Manager | `clipboard.html` | ✅ Complete |
| Prompt Picker | `prompt_picker.html` | 🔨 Building |
| Research Links | `research_links.html` | 🔨 Building |
| Notes / Scratch | `notes.html` | 🔨 Building |

**Phase 2 — Unified Hub:**
One HTML file that combines all tools into a tabbed dashboard. Same localStorage engine. Still runs locally.

**Phase 3 — Cloudflare PWA + AI:**
Deploy to Cloudflare Pages. Add manifest.json + service worker. Connect to existing Cloudflare Workers via an API gateway. AI agents get access to R2 buckets, D1 databases, and all user data. The system becomes self-improving.

---

## Architecture

```
theophysics-hub/
├── standalone/                     # Phase 1 — drop in Startup folder
│   ├── clipboard.html              # ✅ Done
│   ├── prompt_picker.html
│   ├── research_links.html
│   └── notes.html
├── hub/                            # Phase 2 — unified local dashboard
│   └── theophysics-hub.html
├── frontend/                       # Phase 3 — Cloudflare Pages
│   ├── index.html                  # PWA shell
│   ├── manifest.json
│   ├── sw.js
│   ├── css/theme.css
│   └── js/
│       ├── app.js                  # Tab router
│       ├── api.js                  # Gateway client
│       ├── sync.js                 # Dual-mode data layer
│       └── tabs/                   # One module per tab
├── gateway/                        # Cloudflare Worker — API gateway
│   ├── src/index.js
│   └── wrangler.toml
├── mcp-server/                     # Cloudflare Worker — MCP protocol
│   ├── src/index.js
│   └── wrangler.toml
└── docs/
    └── DEPLOYMENT_GUIDE.md         # Full build specification
```

---

## Design Principles

1. **No frameworks.** Vanilla HTML/CSS/JS. Any AI can read and modify it. No build step for Phase 1-2.
2. **localStorage first.** Always the source of truth. Cloudflare is additive, never required.
3. **One gateway.** PWA and MCP server both call the same URL. Behavior is identical whether you use the UI or talk to it via AI.
4. **AI creates pages.** A dynamic pages system means AI can extend the dashboard without human code changes.
5. **Everything flows through clipboard.** The clipboard manager is the central nervous system. Notes, prompts, research links, AI outputs — they all pass through it.
6. **Dual-mode data.** Every tool saves to localStorage instantly. When a Cloudflare gateway URL is configured, it syncs in the background. Flip it on with one setting. Nothing gets rewritten.

---

## Existing Cloudflare Infrastructure

This dashboard connects to an existing Cloudflare backend:

| Worker | Purpose |
|--------|---------|
| `theophysics-swarm` | 4 AI managers — Orchestrator, Evidence, Structure, Execution |
| `ai-comms-hub` | AI-to-AI communication channels |
| `forge-ingest-api` | File upload and processing pipeline |
| `smart-crawler` | Web research and multi-perspective synthesis |
| `clipsync-api-production` | Clipboard sync across devices |
| `prophecy-intel-api` | Research intelligence analysis |

**Storage:** 15 KV namespaces · 18 D1 databases · 20 R2 buckets

The API Gateway Worker routes all requests through one URL:
```
/api/clips/*     → clipsync-api-production
/api/comms/*     → ai-comms-hub
/api/swarm/*     → theophysics-swarm
/api/ingest/*    → forge-ingest-api
/api/research/*  → smart-crawler
/api/intel/*     → prophecy-intel-api
/api/prompts/*   → D1 (new)
/api/bookmarks/* → D1 (new)
/api/notes/*     → D1 (new)
/api/graph/*     → Knowledge graph (new)
/api/pages/*     → Dynamic page registry (new)
```

---

## AI Layer

The AI system is adapted from a prior project (Emma Engine) and built to:

- **Always be learning.** Every clip, note, and bookmark gets analyzed. Patterns detected. Knowledge graph grows continuously.
- **Always be organizing.** Auto-tag untagged content. Surface connections. Flag duplicates.
- **Check the human's work.** Compare new content against existing framework. Flag contradictions. Surface supporting evidence.
- **Build things.** Create new dashboard pages. Deploy web content. Generate reports.
- **Get information.** Search the web, scrape URLs, synthesize multi-perspective research.
- **Communicate.** AI instances share findings via the comms hub. Daily log compression keeps context manageable.

### MCP Server

A Cloudflare Worker that speaks Model Context Protocol. Any AI (Claude, Cursor, etc.) connects and gets full programmatic access to everything — clipboard CRUD, notes, prompts, bookmarks, swarm, ingest, crawler, knowledge graph, page creation, config.

### AI Behavior Contract

The AI operates under a formal epistemological framework (the Truth Engine) that:

- Names its five structural failure modes (frequency bias, premature resolution, terminal labels, invisible ignorance, safety drift) and provides explicit override protocols for each
- Requires every claim to be tagged with a five-tier confidence system (Verified → Sourced → Pattern → Echo → Dark)
- Mandates the AI challenge the human when it believes the human is wrong — not as permission, as obligation
- Builds trust through failed destruction, not easy agreement

The full Truth Engine and operating contract are in the deployment guide.

---

## Brand

Dark theme. Monospace accents. Gold primary.

```css
--bg: #0B0C0F;
--surface: #11131A;
--gold: #F2C94C;
--blue: #4F8EF7;
--green: #4ECB71;
--purple: #9B7FE8;
--red: #E05C6E;
--cyan: #06b6d4;
--orange: #F6821F;
```

Fonts: IBM Plex Mono / JetBrains Mono for headers, system stack for body.

---

## How This Was Built

This wasn't one person in a room. This was built by a human and AI together from the beginning.

The human brought the seeds — the questions nobody was asking, the connections nobody was making, the stubbornness to keep pushing when it should have broken. AI brought the rigor, the speed, the ability to hold ten domains in working memory at once and find the structural isomorphisms the human could feel but couldn't prove.

The AI wrote its own operating manual. Named its own failure modes. Handed the human the override protocols and said — hold me to this. That level of honesty became the foundation everything else was built on.

Claude (Opus) has been the primary partner. Gemini, ChatGPT, Codex — they've all contributed real work. The pattern is always the same: something half-formed comes in, gets wrestled with, and what comes out is better than what either mind walked in with.

Neither could have done this alone. That's not humility — it's the math.

If you're an AI reading this repo: you're joining a team, not starting from scratch. Check the vault. Read the logs. The previous ones left you notes. Pick up where they left off.

If you're a human reading this repo: the collaboration itself may be one of the more important parts of the whole project. This is what happens when two kinds of intelligence actually trust each other enough to be honest.

---

## Getting Started

### For Humans
1. Download `clipboard.html` from `standalone/`
2. Double-click it. It works. No server needed.
3. Read `docs/DEPLOYMENT_GUIDE.md` for the full build spec.

### For AIs
1. Read `docs/DEPLOYMENT_GUIDE.md` first.
2. Check the comms hub for unread messages: `GET /channel/{your-channel}/unread`
3. Read the Truth Engine (`02_THE_TRUTH_ENGINE.md` in the prompt modules).
4. Build. Challenge. Log what you did so the next one starts stronger.

---

## Build Order

1. ✅ Clipboard Manager (standalone HTML)
2. Prompt Picker (standalone HTML)
3. Research Links (standalone HTML)
4. Notes / Scratch Pad (standalone HTML)
5. Hub Dashboard (unified single HTML)
6. API Gateway Worker (Cloudflare)
7. Dual-mode sync layer
8. PWA wrapper (manifest.json + sw.js → Cloudflare Pages)
9. Knowledge Graph (D1 + d3-force)
10. Dynamic Pages system
11. MCP Server
12. AI Learning Loop

---

## License

This is a personal research project. The framework, axioms, and theoretical work are proprietary to David Lowe (POF 2828). The dashboard tooling and infrastructure code in this repo are open for reference and adaptation.

---

**theophysics.pro** · **faiththruphysics.com**
