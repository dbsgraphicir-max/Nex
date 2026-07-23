# Nex — Development Guide

> Practical guide for engineers working on Nex. Pairs with [`ARCHITECTURE.md`](./04-architecture.md) (the *what/why* of the system) and [`CONTRIBUTING.md`](./07-contributing.md) (the *process* for external contributions).

---

## Coding Principles

1. **Optimize for capture-path latency above all else.** Any change touching the capture flow must be measured against the < 3 second target before merge.
2. **Prefer boring, proven technology.** Nex's value is in restraint, not novelty — this applies to code as much as to product surface.
3. **No speculative abstraction.** Don't build configurability, plugin systems, or generic frameworks for requirements that don't exist yet (e.g., do not pre-build a "file attachment" abstraction ahead of its v2 scope).
4. **Local-first is a hard constraint, not an implementation detail.** Every feature must work fully offline unless it is explicitly, unavoidably a network feature (e.g., sync itself, AI transcription).
5. **AI code paths must be structurally optional.** Any AI-layer integration must be behind an interface that can be no-op'd or removed without touching Core or UI layers.
6. **Small, composable modules over large, stateful ones.** Favor pure functions in Core; keep side effects (storage, network, media I/O) isolated at the edges (Data layer).
7. **Every non-negotiable principle in the [Vision doc](./01-nex-product-vision.md#non-negotiable-principles) is a code review gate**, not just a design guideline.

---

## Folder Structure

```
nex/
├── apps/
│   ├── mobile/                 # React Native app shell (Android, future iOS)
│   │   ├── src/
│   │   │   ├── screens/        # Timeline, Capture, Search, NoteDetail
│   │   │   ├── navigation/
│   │   │   └── platform/       # native module bridges (camera, mic, filesystem)
│   │   └── ...
│   ├── desktop/                 # Electron/Tauri app shell (Windows)
│   │   ├── src/
│   │   │   ├── screens/
│   │   │   └── platform/
│   │   └── ...
│   └── backend/                 # Minimal Node.js + PostgreSQL sync API
│       ├── src/
│       │   ├── routes/          # notes, tags, sync
│       │   ├── db/               # Drizzle schema + migrations
│       │   └── services/
│       └── ...
├── packages/
│   ├── core/                    # Platform-agnostic domain logic
│   │   ├── capture/
│   │   ├── search/
│   │   ├── tags/
│   │   └── sync/
│   ├── data/                    # Local-first storage layer
│   │   ├── schema/
│   │   ├── repositories/
│   │   └── sync-client/
│   ├── ui/                      # Shared design system components
│   │   ├── components/
│   │   └── tokens/               # colors, typography, spacing — see DESIGN.md
│   └── ai/                      # Optional AI adapters (v3+)
│       ├── transcription/
│       ├── ocr/
│       └── tagging/
├── docs/                        # This documentation set
└── README.md
```

Each `packages/*` module is independently unit-testable and has no dependency on any `apps/*` shell.

---

## Naming Conventions

- **Files:** `kebab-case` for files and directories (`note-card.tsx`, `capture-sheet.tsx`).
- **Components:** `PascalCase` (`NoteCard`, `CaptureSheet`).
- **Functions/variables:** `camelCase` (`submitCapture`, `activeFilters`).
- **Types/interfaces:** `PascalCase`, no `I` prefix (`Note`, `Tag`, not `INote`).
- **Constants:** `UPPER_SNAKE_CASE` only for true constants (`MAX_TAG_LENGTH`), otherwise `camelCase`.
- **Database columns:** `snake_case`, matching PostgreSQL/SQLite conventions (`created_at`, `device_id`).
- **Branches:** `type/short-description` (`feat/voice-capture-waveform`, `fix/search-date-filter-timezone`).
- **Commits:** [Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`).

---

## State Management Recommendation

Nex's state needs are intentionally modest — a large, generalized global-state framework would be over-engineering relative to the product's scope.

- **Local, ephemeral UI state** (capture sheet open/closed, in-progress text before persistence): component-local state (`useState`/`useReducer` equivalents).
- **Persisted domain state** (notes, tags): owned by the **Data layer** (SQLite-backed repositories), exposed to the UI via reactive queries/subscriptions (e.g., a live-query pattern) so the Timeline updates automatically when the local store changes — including as a result of background sync writes.
- **Cross-cutting app state** (active search filters, current screen): a minimal, single shared store (e.g., a small Zustand-style store or platform-equivalent) — no Redux-scale boilerplate for a product with this few global concerns.
- **Explicit rule:** state management choices must never introduce a delay between "user provided content" and "content is durably saved." Any state layer sitting between the UI and the Data layer must be write-through, not write-behind, for capture actions.

---

## Error Handling

- **Capture must never surface a blocking error to the user.** If local persistence fails (e.g., disk full), the UI must retry transparently and only surface a non-blocking, dismissible notice if content genuinely could not be saved — never a modal that halts the flow.
- **Network and sync errors are silent by default.** Sync failures are logged and retried with backoff; they never interrupt the user's current screen or task.
- **AI errors are always non-blocking and reversible.** A failed transcription, OCR pass, or tag suggestion simply leaves the note in its prior state — the original capture is never mutated destructively by a failed AI operation.
- **User-facing errors follow one pattern:** short, plain-language, dismissible, and actionable only when an action genuinely exists (e.g., "Couldn't reach the server — your notes are saved and will sync later" rather than a raw stack trace or error code).
- **Fail loudly in development, fail quietly in production.** Development builds surface verbose errors and warnings; production builds degrade gracefully and log for later diagnosis (see [Logging](#logging)).

---

## Logging

- **Structured logging only** — every log entry is a structured object (level, module, message, context), never a free-form string, to keep logs queryable as the product scales.
- **Levels:** `debug` (development only), `info` (lifecycle events: app start, sync cycle start/end), `warn` (recoverable issues: a retried failed sync attempt), `error` (unexpected failures requiring attention).
- **No content logging.** Note content, tags, and media are never written to logs, locally or remotely — this is a privacy requirement, not just a style preference (see [AI.md](./09-ai.md) and the vision doc's [AI Philosophy](./01-nex-product-vision.md#ai-philosophy)).
- **Client-side logs stay local** by default; opt-in diagnostic sharing (if ever introduced) must be explicit, scoped, and time-limited.
- **Backend logs** (v2+) are centralized for operational monitoring (error rates, sync latency, API availability) but exclude request bodies containing user content.

---

## Testing Strategy

Testing effort is weighted toward the parts of the system where a regression most directly breaks the product's core promise.

| Layer | Test Type | Priority |
|---|---|---|
| Core domain (capture, search, tags, sync orchestration) | Unit tests, high coverage | Highest — pure logic, cheap to test exhaustively |
| Data layer (repositories, schema, sync client) | Integration tests against a real local SQLite instance | High — correctness of persistence and query behavior is non-negotiable |
| UI components | Component/interaction tests (render, tap, assert state) | Medium — focus on Capture flow and Timeline rendering correctness |
| End-to-end | Scripted flows: capture (each type) → appears in Timeline → found via search | High — these are literally the product's two success metrics |
| Performance | Automated timing assertions on capture-to-save and query-to-result | High — regressions here are regressions of the core value proposition, gated in CI |
| Backend (v2+) | Integration tests for sync conflict scenarios (concurrent edits, offline-then-reconnect, deletion propagation) | High once sync ships |

CI gates on: unit + integration test suites, capture/search performance budgets, and lint/type-check passing. No feature merges if it regresses the < 3 second capture or find budget.

---

## Git Workflow

- **Trunk-based development** on `main`, with short-lived feature branches (`type/short-description`).
- **Pull requests required** for all changes; at least one review approval before merge.
- **CI must pass** (typecheck, lint, unit/integration tests, performance budget checks) before merge is allowed.
- **Squash-merge** to keep `main` history linear and readable, with a Conventional Commits-formatted merge message.
- **Releases are tagged** (`vMAJOR.MINOR.PATCH`) and changelog entries are generated from commit history.
- **No direct commits to `main`**, including for documentation — even docs changes go through review to preserve consistency with the product's identity (see [`CONTRIBUTING.md`](./07-contributing.md)).
- 
