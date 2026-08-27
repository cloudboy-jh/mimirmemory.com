# mimirmemory.com

> Download / landing page for [[Mimir]]

**Domain**: `mimirmemory.com`

**Deploy**: Cloudflare Pages

**Agent**: OpenCode (this is the handoff)

---

## Objective

A one-page download landing page at `mimirmemory.com`. Dark instrument aesthetic aligned with the Mimir dashboard, zero fluff. Someone lands, understands what Mimir is in 5 seconds, and sees the install command.

---

## Product (what Mimir actually is)

From the README:

> **Private memory for coding agents.** Mimir records what your coding agents attempted, which models and files were involved, what failed, and whether the work actually landed. The Worker, storage, and private dashboard run inside your Cloudflare account.

There is no Mimir account, hosted backend, or shared memory service. It's self-hosted on Cloudflare (D1 + R2 + Worker + Durable Object).

**Three inputs to one session record:**
1. Proxied OpenRouter model traffic (full redacted transport exchanges)
2. Reconstructed harness exchanges (OpenCode, Claude Code, Codex, Cursor)
3. Harness lifecycle events (turn summaries, heartbeats, titles, outcomes)

---

## Design

### Vibe
- Dark dashboard aesthetic - Zinc 950 (`#09090b`) canvas, Zinc 900 (`#18181b`) surfaces, and Teal 400 (`#2dd4bf`) signal color
- IBM Plex Sans for interface and prose; IBM Plex Mono only for commands and technical evidence
- Single page, compact. Everything above fold or near-fold on desktop.
- Terminal-style bordered code blocks
- No animations, no stock photos, no gradients

### Structure (top to bottom)

#### 1. Header bar
- Left: Mimir pixel-art wordmark from `assets/mimir-readme.png`
- Right: GitHub button - SVG GitHub icon + "GitHub", links to `https://github.com/cloudboy-jh/Mimir`

#### 2. Hero
- **Private memory for coding agents** - main tagline
- Sub-line: *Records what your agents attempted, which models and files were involved, what failed, and whether the work landed.*

#### 3. Install block (terminal-style bordered box)

First-time bootstrap:
```bash
go run github.com/cloudboy-jh/mimir/cmd/mimir@latest install
mimir setup
```

Copy-to-clipboard on each code block. Below the commands, a small note:

```
Requirements: Cloudflare account, OpenRouter API key, Go 1.25+, Node.js 22 + npm, Bun.
To connect another machine: mimir login
```

#### 4. Quickstart / command reference (collapsible or compact grid)

Organized into logical groups:

```
# install / setup
  mimir install                  reconcile managed local artifacts
  mimir setup [--quick]          provision and deploy Mimir
  mimir login                    connect another machine

# use
  mimir list [filters]           browse recent sessions
  mimir search <query>           search saved session memory
  mimir session get <id>         inspect one session record
  mimir session outcome <id>     record an evidenced work result

# manage
  mimir dashboard                open the private dashboard
  mimir tui                      open terminal UI
  mimir doctor                   validate deployment and integrations
  mimir deploy                   deploy Worker and dashboard changes
  mimir update                   update Mimir and managed integrations
```

Each command row gets a copy-to-clipboard on hover (just the command part, not the description).

#### 5. Footer
- `◆ mimir` in dimmed green, centered

---

## Technical requirements

### Static files
- Static `.html` plus the supplied wordmark and favicon assets - no build step, no framework, no JS dependencies
- Inline CSS (no external stylesheets except Google Fonts for IBM Plex Sans and IBM Plex Mono)
- Vanilla JS only for copy-to-clipboard (`navigator.clipboard.writeText()`)

### Copy-to-clipboard
- Each code block and command row gets a copy button on hover
- On click: copies text, shows "copied ✓" feedback

### Responsive
- Mobile-friendly - stacks vertically, code blocks `overflow-x: auto`
- Font scales on mobile

### Performance
- Zero tracking, no analytics, no third-party requests (except Google Fonts)
- Target: sub-50KB for local page assets, sub-100ms first paint

---

## Content (exact)

### Tagline
> Private memory for coding agents

### Sub-line
> Mimir records what your coding agents attempted, which models and files were involved, what failed, and whether the work actually landed.

### Install
```bash
go run github.com/cloudboy-jh/mimir/cmd/mimir@latest install
mimir setup
```

### Quickstart commands
```
mimir install     - reconcile managed local artifacts
mimir setup       - provision and deploy Mimir
mimir login       - connect another machine
mimir search      - search saved session memory
mimir session get - inspect a session record
mimir dashboard   - open the private dashboard
mimir doctor      - validate deployment
```

---

## Implementation notes

- File: `index.html`
- Deploy to Cloudflare Pages with `mimirmemory.com` custom domain
- No redirects, no subpages, no JS framework
- Dark mode only (no light toggle)

---

## Visual reference

Feels like the Mimir dashboard - a Zinc-black canvas, flat bordered surfaces, compact mechanical controls, IBM Plex typography, and teal used only as a signal. The pixel-art wordmark carries the identity; commands remain monospace evidence.

---

## Deliverable

An `index.html` plus optimized wordmark and favicon assets, written and pushed to a repo so Cloudflare Pages picks them up. Openable in a browser in 2 minutes - someone knows what Mimir is, how it works, and how to install it.
