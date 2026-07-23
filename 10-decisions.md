# Nex — Decision Log

> A running record of significant product and architectural decisions, with rationale. New entries are appended chronologically; existing entries are never edited retroactively — superseding decisions reference the ones they replace.

Each entry follows a lightweight ADR (Architecture Decision Record) format: **Context → Decision → Rationale → Alternatives Considered → Status**.

---

## ADR-001 — Capture has zero mandatory fields

- **Context:** Traditional note apps require a title, folder, or category before saving, which introduces friction and causes ideas to be lost.
- **Decision:** No field is ever mandatory during capture. Title, folder, and tags are all optional and can be added later, if at all.
- **Rationale:** Directly serves the "Capture First" pillar of the product philosophy; friction at capture time is the core problem Nex exists to solve.
- **Alternatives Considered:** Optional-but-suggested title field pre-filled with a timestamp — rejected because even a pre-filled field invites a decision ("should I change this?").
- **Status:** Accepted, v1.

---

## ADR-002 — No Save button; auto-save on content presence

- **Context:** A visible Save button implies the possibility of losing unsaved work and adds one more required action to capture.
- **Decision:** Notes persist automatically as soon as they contain content (first keystroke, recording stop, confirmed photo). There is no Save action anywhere in the capture flow.
- **Rationale:** Removes both the interaction cost and the cognitive overhead of wondering "did I save that?" — directly supporting user trust, a core value.
- **Alternatives Considered:** Debounced auto-save with a visible "Saved" indicator — partially adopted (see ADR-006) but without ever exposing a manual Save control.
- **Status:** Accepted, v1.

---

## ADR-003 — Timeline as the only home screen, no default folders

- **Context:** Folder-first organization (as in most note apps) forces a categorization decision before or during capture.
- **Decision:** All notes land in a single, reverse-chronological Timeline. No default or system-created folders exist.
- **Rationale:** Encodes "Organize Later" structurally — there is no organizational scaffold to interact with at all unless the user creates one via tags.
- **Alternatives Considered:** A default "Inbox" folder with the option to create others — rejected as functionally redundant with the Timeline itself and a source of user confusion ("what's the difference between Inbox and Timeline?").
- **Status:** Accepted, v1.

---

## ADR-004 — Tags are the only organizational primitive in v1

- **Context:** Users will eventually want *some* way to group related captures, but any structure added at v1 risks recreating folder-like complexity.
- **Decision:** Tags — flat, freeform, optional, many-to-many — are the sole organizational tool in the MVP. No folders, notebooks, nested tags, or projects.
- **Rationale:** Tags can be applied after the fact with zero impact on capture speed, satisfying "Organize Later" while still giving users a lightweight structuring option.
- **Alternatives Considered:** Nested/hierarchical tags — rejected for v1 as unnecessary complexity relative to the MVP's scale and philosophy of simplicity (see [Vision — Product Boundaries](./01-nex-product-vision.md#product-boundaries)).
- **Status:** Accepted, v1. Revisit only if user research at scale demonstrates flat tags are insufficient.

---

## ADR-005 — Voice notes are searchable only by tag/date/type in v1, not by keyword

- **Context:** The original product concept introduced full-text search as a core pillar while simultaneously excluding speech-to-text from MVP scope — a direct contradiction, since a voice note has no text body without transcription.
- **Decision:** In v1 and v2, voice notes are excluded from keyword search and are discoverable only via tag, date, and content-type filters. The UI explicitly labels voice notes as "searchable by tag/date only."
- **Rationale:** Resolves the contradiction honestly rather than either (a) silently shipping broken search expectations, or (b) pulling speech-to-text into the MVP and inflating its scope and timeline.
- **Alternatives Considered:**
  1. Include basic on-device speech-to-text in v1 — rejected due to added complexity, quality risk, and scope creep that would delay the core capture/timeline/search MVP.
  2. Silently omit the limitation from the UI — rejected as a trust violation; users would form an incorrect mental model of search.
- **Status:** Accepted, v1. Superseded in effect (not retroactively) by ADR-009 when transcription ships in v3.

---

## ADR-006 — Local-first architecture with sync-ready schema from day one

- **Context:** The user's original need (Android + Windows, later iOS, with full sync) is a v2 goal, but retrofitting sync onto a schema not designed for it typically requires a costly rewrite (adding UUIDs, timestamps, conflict resolution metadata after the fact).
- **Decision:** Every record — from v1 — carries a UUID, `created_at`/`updated_at` timestamps, `device_id`, `sync_version`, and a soft-delete (`deleted_at`) field, even though sync is inactive until v2. A minimal backend (Node.js + PostgreSQL) exists from v1 as dormant infrastructure.
- **Rationale:** Ensures v2 sync is additive — new capability, same schema — rather than a breaking migration. Matches the mandate that sync must be architected from day one even if not user-facing in v1.
- **Alternatives Considered:** Ship v1 with a simple auto-increment local schema and migrate later — rejected because migrating existing user data to sync-compatible identifiers post-hoc is materially riskier and more expensive than doing it correctly from the start.
- **Status:** Accepted, v1.

---

## ADR-007 — Sync ships as the first item of v2, not the last

- **Context:** Sync is often deprioritized to the end of a release because it's technically complex, but for Nex, unsynced multi-device use directly perpetuates the product's founding problem (scattered, lost ideas).
- **Decision:** Real Android ⇄ Windows sync is the first feature delivered in v2, ahead of generic file attachments and the iOS client.
- **Rationale:** Without sync, a user who captures on their phone and needs it on their desktop is exactly as stuck as they were before adopting Nex — the core value proposition is incomplete until sync exists.
- **Alternatives Considered:** Ship generic file attachments first as a "quick win" — rejected because it doesn't address the more painful, more foundational gap.
- **Status:** Accepted, planned for v2.

---

## ADR-008 — Generic file attachments deferred out of v1

- **Context:** A fourth capture type ("generic file") was part of the original concept but requires UX decisions (preview strategy, size limits, supported file types) that conflict with the "zero decisions at capture time" principle if rushed.
- **Decision:** Generic file attachments are moved to v2, to be designed deliberately rather than bolted onto the v1 capture flow.
- **Rationale:** Protects v1 scope and development velocity, and avoids shipping a capture type whose UX would require exactly the kind of in-the-moment decision-making Nex is built to eliminate.
- **Alternatives Considered:** Ship a minimal, size-capped generic file type in v1 — rejected as scope creep with a poor cost/benefit ratio relative to the MVP's two core goals.
- **Status:** Accepted, deferred to v2.

---

## ADR-009 — AI capabilities deferred to v3, after capture (v1) and sync (v2) are solid

- **Context:** AI (transcription, OCR, semantic search, tagging, summarization, related notes) could plausibly be introduced earlier, but doing so risks distracting from proving the core, non-AI product value first.
- **Decision:** All AI capabilities ship in v3, sequenced after the Timeline/capture/search MVP (v1) and cross-device sync (v2) are both stable.
- **Rationale:** Speed and reliability of capture and sync are the product's foundation; AI is explicitly optional and additive, and should only be layered onto a proven base — consistent with "AI never slows down capture" and "AI is optional."
- **Alternatives Considered:** Introduce lightweight on-device tag suggestions earlier (e.g., v1.x) — rejected to keep the v1/v2 milestones focused and to avoid partial, inconsistent AI coverage before the full intelligence layer is designed holistically (see [`AI.md`](./09-ai.md)).
- **Status:** Accepted, planned for v3.

---

## ADR-010 — Monochrome, minimal visual design with no categorical color coding

- **Context:** Many note/task apps use color to encode categories, priorities, or tags, which can subtly reintroduce organizational decision-making at the point of interaction.
- **Decision:** Nex's UI uses a strictly black-and-white (plus grayscale) palette in both light and dark modes; tags and content types are never color-coded.
- **Rationale:** Reinforces the "light," non-software feeling described in the UX philosophy, and prevents color from becoming an implicit, uncontrolled categorization system users would otherwise have to maintain.
- **Alternatives Considered:** A small palette of accent colors for tags — rejected as inconsistent with the minimal, decision-free design philosophy and as an unnecessary maintenance burden for users.
- **Status:** Accepted, v1.

---

## ADR-011 — Content-type filter is part of the single search surface, not a separate mode

- **Context:** The original concept considered a distinct search mode per content type, which would fragment the search UI into multiple screens/flows.
- **Decision:** Content-type (text/voice/photo) is implemented as a filter layered onto the same tag/date search screen, not a separate search mode.
- **Rationale:** Keeps the v1 search UI to a single, learnable surface, consistent with the "every feature learnable in under 30 seconds" principle, and reduces implementation and maintenance complexity.
- **Alternatives Considered:** Separate top-level tabs per content type — rejected as unnecessary UI fragmentation for what is, functionally, just another filter.
- **Status:** Accepted, v1.
