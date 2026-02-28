# Contributing to Paperly

Thank you for your interest in contributing! Paperly is a single-file web app — no build tools, no dependencies to install. Here's everything you need to know.

---

## Getting Started

```bash
git clone https://github.com/YOUR_USERNAME/AI-junk-journal-copilot.git
cd AI-junk-journal-copilot
open index.html   # Just open it in a browser
```

Make your changes to `index.html`, refresh the browser. That's the entire dev workflow.

---

## What to Work On

Check the [Issues](../../issues) tab for open bugs and feature requests. Issues labelled `good first issue` are the best starting point.

---

## Submitting a Pull Request

1. **Fork** the repo and create a branch: `git checkout -b fix/your-fix-name`
   ```bash
   git clone https://github.com/YOUR_USERNAME/AI-junk-journal-copilot.git
   ```
2. Make your changes to `index.html`
3. Test manually in at least one browser (Chrome or Firefox)
4. Write a clear PR description:
   - What was the problem?
   - What does your change do?
   - How did you test it?
5. Open the PR against the `main` branch

---

## Code Style

- **ES2020+** — use `const`/`let`, arrow functions, optional chaining, template literals
- **`'use strict'`** is set — don't introduce undeclared globals
- **No external dependencies** — the app must work from a local file system with no internet (except Supabase and the Anthropic API for opt-in features)
- **Single file** — do not split into multiple files unless there's a very compelling reason and it's discussed in an issue first
- **Meaningful variable names** — the codebase uses short names in tight loops but descriptive names for functions and state

---

## Reporting Bugs

Open an issue using the Bug Report template. Please include:
- Browser and OS
- Steps to reproduce
- What you expected vs. what happened
- Console errors if any (F12 → Console tab)

---

## Suggesting Features

Open an issue using the Feature Request template. Good feature requests explain the user problem being solved, not just the solution.

---

## Code of Conduct

Be kind. Be constructive. Assume good intent.
