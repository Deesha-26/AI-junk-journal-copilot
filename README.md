# Paperly ✦

**Your memories, made beautiful.**

Paperly is an AI-powered junk journal web app. Drop a photo, and Claude reads the light, the feeling, the story — then writes your journal page for you. Add washi tape, postmarks, botanical stickers, and torn scrap paper. Every memory, made beautiful.

![Paperly Landing](https://img.shields.io/badge/status-MVP-amber) ![License](https://img.shields.io/badge/license-MIT-green) ![Single File](https://img.shields.io/badge/architecture-single--file-blue)

---

## ✨ Features

- **AI-powered writing** — Upload any photo, Claude analyzes it and generates a title, caption, memory quote, date, and location in your chosen voice
- **5 aesthetic styles** — Vintage, Dark Academia, Botanical, Faded Summer, Moody
- **Torn paper effects** — Procedurally generated clip-paths give every photo authentic torn edges
- **Washi tape & ephemera** — Drag and position tape, postmarks, botanical stickers, stamps, and handwritten text overlays
- **Collage layers** — Stack up to 4 photos per page with natural offsets and tilt
- **Torn paper mode** — Scrap paper quote block with realistic washi tape hold
- **Cloud sync** — Sign in with Supabase to sync journals across devices
- **Works offline** — Local-first with localStorage fallback; Supabase stub activates if CDN fails
- **Share & export** — Generate a shareable link or download a PNG of your page
- **Demo mode** — 4 pre-built atmospheric pages to explore before signing up

---

## 🚀 Quick Start

### Option 1: Just open it (no setup needed)

```bash
git clone https://github.com/YOUR_USERNAME/AI-junk-journal-copilot.git
cd AI-junk-journal-copilot
open index.html   # macOS
# or: xdg-open index.html  (Linux)
# or: double-click index.html in your file explorer
```

That's it. The app runs entirely in the browser with no build step.

### Option 2: Deploy to GitHub Pages (1 minute)

1. Fork this repo
2. Go to **Settings → Pages**
3. Source: `Deploy from a branch`, branch: `main`, folder: `/` (root)
4. Visit `https://YOUR_USERNAME.github.io/AI-junk-journal-copilot`

### Option 3: Deploy to Netlify / Vercel (drag and drop)

Drag the `index.html` file into [Netlify Drop](https://app.netlify.com/drop) or [Vercel](https://vercel.com/new). Done.

---

## 🔑 Configuration

### Claude AI (for AI suggestions)

The AI suggestions feature requires an Anthropic API key. Once you have one:

1. Open the app
2. In the editor right panel, find **🔑 CLAUDE API KEY**
3. Paste your key — it's saved to `localStorage` on your device only

Get an API key at [console.anthropic.com](https://console.anthropic.com).

> **Note:** The API key is stored in your browser's localStorage and is never sent anywhere except directly to the Anthropic API. No server involved.

### Supabase (for cloud sync, optional)

Cloud sync is optional. The app works fully offline without it.

To enable cloud sync with your own Supabase project:

1. Create a free project at [supabase.com](https://supabase.com)
2. Create a table:
```sql
create table journals (
  id text primary key,
  user_id uuid references auth.users not null,
  data jsonb not null,
  updated_at timestamptz default now()
);

alter table journals enable row level security;

create policy "Users can manage their own journals"
  on journals for all
  using (auth.uid() = user_id);
```
3. In `index.html`, update lines with `SUPA_URL` and `SUPA_KEY`:
```js
const SUPA_URL = 'https://YOUR_PROJECT.supabase.co';
const SUPA_KEY = 'YOUR_ANON_KEY';
```

If you skip this step, the app uses a local stub — sign-in creates a local session, journals save to localStorage only.

---

## 🏗️ Architecture

Paperly is deliberately a **single HTML file** — no build toolchain, no node_modules, no bundler. Everything is self-contained.

```
index.html
├── <style>          CSS (custom properties, responsive, print)
├── <script>         Supabase offline stub
├── <script src>     Supabase CDN (falls back to stub on failure)
└── <script>         App JS (~900 lines, 'use strict')
    ├── State        S = { journals, jid, pidx, preset, scrapMode, isDemo }
    ├── Storage      localStorage (images as data URLs) + Supabase cloud sync
    ├── Auth         Supabase email/password
    ├── Views        Library (landing/shelf) ↔ Editor
    ├── Rendering    Procedural canvas art, torn clip-paths, washi tape
    ├── AI           Anthropic claude-sonnet-4-* via direct browser API call
    └── Demo         4 atmospheric scenes generated via HTML Canvas
```

### Key design decisions

| Decision | Reason |
|---|---|
| Single file | Zero setup, instant deploy, email-able, works from filesystem |
| Direct Anthropic API call | No backend needed; user provides their own key |
| Canvas-generated demo images | No external image dependencies; works offline |
| localStorage for images | Avoids server storage costs for MVP |
| Seeded RNG for visual effects | Deterministic torn edges / tape positions per page |

---

## 📁 File Structure

```
AI-junk-journal-copilot/
├── index.html          The entire application
├── README.md           This file
├── LICENSE             MIT License
├── CONTRIBUTING.md     How to contribute
├── .gitignore          Standard web .gitignore
└── .github/
    └── ISSUE_TEMPLATE/
        ├── bug_report.md
        └── feature_request.md
```

---

## 🛣️ Roadmap

- [ ] Export to PDF
- [ ] Custom fonts for page text
- [ ] More ephemera types (tickets, maps, envelopes)
- [ ] Page templates / layouts
- [ ] Multi-page printing
- [ ] Collaborative journals (share with edit access)
- [ ] Mobile app wrapper (PWA)
- [ ] Import from Instagram / Google Photos

---

## 🤝 Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md).

**Quick contribution guide:**
- Bug fixes: open a PR with a clear description of what was broken and how you fixed it
- New features: open an issue first to discuss approach
- The app is a single file — keep it that way for now

---

## 📄 License

MIT — see [LICENSE](LICENSE).

---

## 🙏 Acknowledgements

- [Anthropic Claude](https://anthropic.com) for AI text generation
- [Supabase](https://supabase.com) for auth and sync
- Google Fonts: Cormorant Garamond, Caveat, Special Elite, Crimson Pro
