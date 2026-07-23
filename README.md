# Nex

> **Capture in Seconds. Find in Seconds.**

Nex is a personal capture tool — the **inbox for the human mind**. It does two things exceptionally well: capture anything in under three seconds, and find it again in under three seconds.

Nex is **not** a knowledge management system, a project-management tool, or a second-brain platform. It is the **doorway** to a second brain: the fastest possible place to drop a thought, leaving organization for later.

> *Capture First. Organize Later. Find Instantly.*

---

## Introduction

Most note-taking apps make you open the app, create a note, name it, choose a folder, and press **Save**. By the time that's done, the idea is gone. Nex removes that friction.

- **One tap to capture.** No title. No folder. No Save button.
- **One timeline.** Everything flows into a single time-ordered stream.
- **Instant search.** Find anything in under three seconds.
- **Local-first.** Your data lives on your device. Offline by default.

---

## Features (v1 — MVP)

- ⚡ **Quick Capture** — text, audio, and photo, with auto-save and no Save button.
- 🗓️ **Timeline** — a single, minimal, newest-first stream of everything you captured.
- 🔍 **Instant Search** — by text, tag, date, and content type.
- 🏷️ **Tags** — the only organization tool, and entirely optional.
- 📴 **Offline-first** — fully functional with no connection.
- 🔒 **Private** — local-first; nothing leaves your device in v1.

> **Honest limitation:** audio notes have no transcript in v1, so they are searchable by **tag or date only**. Transcription arrives in v3.

---

## Philosophy

Nex is built on three non-negotiable principles:

1. **Capture First.** Capturing must be faster than thinking. While capturing, you make zero decisions.
2. **One Inbox.** Everything lives in one timeline. Organize later — optionally.
3. **Find Instantly.** If you can't find it, capturing it was worthless.

Core values: **speed over features, simplicity over power, restraint over feature creep.** If a feature slows down capture, it does not belong in Nex.

See [01-product-vision.md](./01-product-vision.md) and [05-design.md](./05-design.md) for the full philosophy.

---

## Tech Stack (Recommended)

Nex is local-first, cross-platform (Android, Windows, iOS), and intentionally lightweight.

| Layer | Recommendation | Why |
| --- | --- | --- |
| **App shell / shared logic** | TypeScript + React | One language across platforms |
| **Desktop** | Electron or Tauri (wrapper) | Reuse the same UI/logic |
| **Mobile** | React Native or Capacitor | Shares codebase with desktop |
| **Local database** | SQLite (via a reactive driver) | Fast, embedded, offline-first |
| **Backend (v2 sync)** | Minimal Node/TypeScript service | Thin sync endpoint |
| **Styling** | Tailwind CSS | Minimal, consistent, fast |
| **AI (v3, optional)** | Provider-agnostic adapters | Keep AI optional and swappable |

> The key architectural choice is **local-first**: the local SQLite store is the source of truth, and any backend is a *sync* layer, never a *dependency*.

See [04-architecture.md](./04-architecture.md) and [06-development.md](./06-development.md).

---

## Project Structure

```
nex/
├── docs/                       # This documentation (source of truth)
│   ├── 01-product-vision.md
│   ├── 02-product-specification.md
│   ├── 03-readme.md
│   ├── 04-architecture.md
│   ├── 05-design.md
│   ├── 06-development.md
│   ├── 07-contributing.md
│   ├── 08-roadmap.md
│   ├── 09-ai.md
│   └── 10-decisions.md
├── src/
│   ├── app/                    # UI surfaces (timeline, capture, search)
│   ├── capture/                # Quick-capture flows (text/audio/photo)
│   ├── search/                 # Search + filters
│   ├── store/                  # Local-first data layer (SQLite + repository)
│   ├── sync/                   # Sync adapter (inactive in v1; active in v2)
│   ├── ai/                     # Optional AI adapters (v3)
│   ├── ui/                     # Reusable components, design system
│   └── shared/                 # Types, utils, domain models
└── ...
```

---

## Roadmap

- **v1 — Fastest capture experience** ✅ *(target)* — Timeline, text/audio/photo capture, tags, instant local search, sync-ready local-first architecture.
- **v2 — Everywhere** — Cross-device sync (Android, Windows, iOS) as the headline; generic file capture.
- **v3 — Intelligence** — Transcription, semantic search, OCR, tag suggestions, summarization, related notes.

See [08-roadmap.md](./08-roadmap.md).

---

## Contribution

Nex is intended to grow as an open-source project. Contributions that **make capture faster or the surface simpler** are welcome; contributions that add complexity to the capture flow are not.

- Read [07-contributing.md](./07-contributing.md) before opening a PR.
- Respect the [core principles](./01-product-vision.md#non-negotiable-principles): zero friction, no Save button, timeline-first.
- Keep PRs small and focused.

---

## License

Nex is released under the **MIT License** — permissive, simple, and friendly to individuals and companies alike.

```
MIT License

Copyright (c) 2026 Nex contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.
```

---

> *Capture it — before you forget it.*
> 
