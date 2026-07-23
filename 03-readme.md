# Nex

**Capture in Seconds. Find in Seconds.**

Nex is a local-first, minimal capture tool — the inbox for your mind. Instead of asking you to choose a folder, a template, or hit "Save," Nex gets out of your way: tap, capture, done. Organize later, if you ever need to.

> Nex is not a knowledge base, not a project manager, not another Notion or Obsidian. It's the fastest possible front door into whatever system you use to think.

---

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Philosophy](#philosophy)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Roadmap](#roadmap)
- [Documentation](#documentation)
- [Contribution](#contribution)
- [License](#license)

---

## Introduction

Every second between having a thought and capturing it is a second in which that thought might disappear. Most note-taking apps optimize for organizing information well — Nex optimizes for capturing it *fast*.

Nex's entire product surface is built around two guarantees:

- **Capture takes less than 3 seconds.**
- **Finding a capture takes less than 3 seconds.**

Everything else — tags, filters, sync, AI — exists only to serve those two guarantees, never to compete with them.

Read the full story in [`Nex Product Vision`](./01-nex-product-vision.md).

---

## Features

### Available in v1 (MVP)

- ⚡ **One-tap capture** — a single "+" button branches into three capture types: text, voice, photo.
- 🔇 **Zero-friction recording** — voice capture starts recording immediately, no "press to start" step.
- 🖼️ **Instant photo capture** — camera or gallery, two taps max.
- 💾 **No Save button** — every capture is persisted automatically the moment it has content.
- 🗂️ **Optional tags** — the only organizational tool, entirely opt-in, applied after the fact.
- 🕒 **Unified timeline** — every capture lands in one reverse-chronological stream, no default folders.
- 🔍 **Fast search** — full-text search on text notes, plus tag / date / content-type filters.
- 📡 **Offline-first** — every core flow works with zero network connection.

### Planned

- 🔄 Real cross-device sync (Android ⇄ Windows, then iOS) — see [`v2`](./08-roadmap.md#v2--sync--continuity)
- 🎙️ Speech-to-text transcription for voice notes — see [`v3`](./08-roadmap.md#v3--the-intelligence-layer)
- 🔡 OCR for photo notes
- 🏷️ AI-assisted tag suggestions
- 🧠 Semantic search
- ✂️ Summarization & related notes

Full detail in [`Nex Product Specification`](./02-nex-product-specification.md) and [`ROADMAP.md`](./08-roadmap.md).

---

## Philosophy

Three rules drive every product and engineering decision:

1. **Capture First** — the user never decides *where* something goes while capturing it; they just capture.
2. **Organize Later** — everything enters a single timeline; tagging is optional and deferred.
3. **Find Instantly** — search is a first-class pillar, not an afterthought.

See [`Nex Product Vision`](./01-nex-product-vision.md) for the full philosophy and non-negotiable principles.

---

## Tech Stack

Nex's stack is chosen to support a **local-first, offline-first, cross-platform** product without locking the architecture into a rewrite when sync ships in v2.

| Layer | Recommendation | Why |
|---|---|---|
| **Mobile (Android, future iOS)** | React Native | Single codebase across mobile platforms; mature offline storage ecosystem |
| **Desktop (Windows)** | Electron or Tauri wrapping the same web core | Reuses UI layer; Tauri preferred long-term for footprint/performance |
| **Shared UI core** | React + TypeScript | One component/business-logic layer shared across web, desktop, and (via React Native) mobile |
| **Local storage** | SQLite (via a platform-appropriate driver) | Durable, transactional, queryable local-first storage; trivial full-text search via FTS5 |
| **State management** | Lightweight local-first store (see [`DEVELOPMENT.md`](./06-development.md)) | Predictable, minimal, no over-engineering |
| **Backend (minimal, v1 dormant)** | Node.js + PostgreSQL, exposed via a small REST/JSON API | Provides the sync-ready contract described in [`ARCHITECTURE.md`](./04-architecture.md) without being load-bearing in v1 |
| **Sync transport (v2)** | HTTPS + incremental delta sync | Simple, debuggable, works well with soft-deletes and `updated_at`-based conflict resolution |
| **AI services (v3, optional)** | On-device or server-side speech-to-text/OCR provider, pluggable | Keeps AI optional and swappable; never blocks capture |

This is a recommendation, not a hard requirement — but any substitution must preserve the local-first, offline-first, minimal-footprint constraints above.

---

## Project Structure

A representative structure for the shared core and platform shells (see [`DEVELOPMENT.md`](./06-development.md) for full conventions):

```
nex/
├── apps/
│   ├── mobile/            # React Native shell (Android, future iOS)
│   ├── desktop/           # Electron/Tauri shell (Windows)
│   └── backend/           # Minimal Node.js + PostgreSQL API (dormant in v1)
├── packages/
│   ├── core/              # Shared business logic (capture, search, tags)
│   ├── data/              # Local-first storage layer, schema, sync-ready models
│   ├── ui/                # Shared design system components
│   └── ai/                # Optional AI adapters (transcription, OCR, tagging) — v3+
├── docs/                  # This documentation set
└── README.md
```

---

## Getting Started

> Nex's product implementation ships per-platform (mobile/desktop clients + backend). Refer to each app package's own setup instructions once those packages are scaffolded.

General workflow:

```bash
# install dependencies at the workspace root
npm install

# run the shared core's tests
npm run test --workspace=packages/core

# start the desktop shell in development mode
npm run dev --workspace=apps/desktop
```

See [`DEVELOPMENT.md`](./06-development.md) for coding standards, folder conventions, and testing strategy.

---

## Roadmap

| Version | Focus |
|---|---|
| **v1** | Fastest capture experience: timeline, text/voice/photo capture, tags, search |
| **v2** | Sync & continuity: real Android ⇄ Windows sync, generic file attachments, iOS |
| **v3** | Intelligence layer: speech-to-text, OCR, tag suggestions, semantic search, summarization, related notes |

Full detail in [`ROADMAP.md`](./08-roadmap.md).

---

## Documentation

| Document | Purpose |
|---|---|
| [`Nex Product Vision`](./01-nex-product-vision.md) | Why Nex exists, mission, principles |
| [`Nex Product Specification`](./02-nex-product-specification.md) | What is being built, requirements, data model |
| [`ARCHITECTURE.md`](./04-architecture.md) | Technical architecture, local-first design, sync |
| [`DESIGN.md`](./05-design.md) | Design language, UI principles, accessibility |
| [`DEVELOPMENT.md`](./06-development.md) | Developer guide, conventions, testing |
| [`CONTRIBUTING.md`](./07-contributing.md) | How to contribute |
| [`ROADMAP.md`](./08-roadmap.md) | Version plan, MVP through v2.x+ |
| [`AI.md`](./09-ai.md) | AI strategy and boundaries |
| [`DECISIONS.md`](./10-decisions.md) | Architectural and product decision log |

---

## Contribution

Contributions are welcome and encouraged. Please read [`CONTRIBUTING.md`](./07-contributing.md) before opening a pull request — in particular, note that any contribution must preserve Nex's core identity (see [Philosophy](#philosophy)). Features that add friction to capture will not be accepted, regardless of technical quality.

---

## License

Nex is released under the [MIT License](./LICENSE). You are free to use, modify, and distribute it, provided the original copyright notice is retained.
