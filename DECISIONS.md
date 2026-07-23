# Nex — Decision Records (ADR)

> Architectural and product decisions, with rationale. The *why* behind the *what*.

**Status:** Living document · **Owner:** Product & Engineering · **Last updated:** 2026

These records follow a lightweight ADR format: **Context → Decision → Consequences.** They exist so future contributors understand *why* Nex is built a certain way — and so we don't relitigate settled questions.

---

## ADR-0001 — Local-first architecture

**Status:** Accepted

### Context
The core problem is lost and scattered ideas. A cloud-dependent app fails to capture the moment connectivity drops, and centralizes private data unnecessarily. The product must work instantly and offline.

### Decision
Make the **local store the single source of truth**. All reads and writes hit local SQLite first; the app is fully functional offline. Any backend is a *sync* layer, never a *dependency*.

### Consequences
- ✅ Capture and search always work, offline, with sub-second latency.
- ✅ Strong privacy by default in v1.
- ⚠️ Requires a sync-ready data model from day one (see ADR-0002) so v2 needs no rewrite.
- ⚠️ Cross-device coherence is deferred to v2.

---

## ADR-0002 — Sync-ready data model from v1

**Status:** Accepted

### Context
Real cross-device sync is scoped to v2, but the product's data is only valuable if it can later be coherent across devices. Waiting until v2 to design for sync would force a painful migration.

### Decision
Every record carries the full sync contract **from v1**, even though sync is inactive: stable client-generated `id` (UUID v7), `created_at`, `updated_at`, monotonic `rev`, soft-delete `deleted_at`, and `device_id`. Media stores a content `media_hash`.

### Consequences
- ✅ v2 sync requires **no schema migration or rewrite**.
- ✅ Soft-delete tombstones make deletions sync-safe.
- ⚠️ Slightly more fields to maintain in v1 — an acceptable, intentional cost.

---

## ADR-0003 — Resolve roadmap ambiguity for intelligent features

**Status:** Accepted

### Context
The original product notes listed several intelligent features (transcription, OCR, semantic search, tag suggestions, summarization, related notes) under an ambiguous "v1" heading, while other sections clearly state transcription is **v3** and sync is **v2**. This created a contradiction.

### Decision
Resolve the contradiction in favor of the explicit, repeated statements elsewhere in the spec:
- **v1:** timeline, capture (text/audio/photo), tags, search, local-first sync-ready storage. **No AI.**
- **v2:** cross-device sync (headline, first), generic file capture.
- **v3:** transcription (→ audio becomes text-searchable), semantic search, OCR, tag suggestions, summarization, related notes.

### Consequences
- ✅ A single, consistent roadmap across all documents.
- ✅ v1 stays maximally light and fast.
- ⚠️ Users must accept the v1 audio limitation (tag/date-only search), mitigated by honest UI labeling.

---

## ADR-0004 — Audio is tag/date-only searchable in v1

**Status:** Accepted

### Context
Search is a core pillar, yet v1 has no speech-to-text. Without transcripts, audio notes have no searchable text — a real tension with the "find instantly" promise.

### Decision
In v1, audio notes are found **only by tag or date**. The UI states this limitation plainly (e.g., a "Searchable by tag/date only" label on each audio note) so users form correct expectations. Transcription in v3 removes the limitation.

### Consequences
- ✅ Honest UX; no false expectations about audio search.
- ✅ Keeps v1 scope small (no transcription/STT pipeline).
- ⚠️ Audio isn't content-searchable until v3 — an accepted, clearly-communicated trade-off.

---

## ADR-0005 — Only three capture types in v1; generic file deferred to v2

**Status:** Accepted

### Context
A fourth "generic file" capture type is useful but introduces UX decisions (preview, size limits, type handling) that conflict with "no decisions at capture time" and would slow both development and the capture experience.

### Decision
Ship **text, audio, and photo** only in v1. Defer **generic file** capture to v2, where the preview/size/type UX can be designed deliberately.

### Consequences
- ✅ v1 capture stays decision-free and fast.
- ✅ Better, focused search quality (fewer content types to handle).
- ⚠️ Power users wait until v2 for arbitrary files — acceptable for an inbox tool.

---

## ADR-0006 — Tags are the only organization tool; no folders

**Status:** Accepted

### Context
Folders, notebooks, and hierarchies add decisions at and after capture, conflicting with "capture first / organize later" and adding UI weight.

### Decision
**Tags are the sole organization primitive** in v1, and they are **always optional**. There are no folders, notebooks, or hierarchies. The timeline is the single home.

### Consequences
- ✅ Zero organization friction; learnable in seconds.
- ✅ Simpler, lighter data model and UI.
- ⚠️ Users wanting deep structure must use tags and (later) external tools — consistent with Nex being the *inbox*, not the *system*.

---

## ADR-0007 — Content-type filter over the search, not a separate search mode

**Status:** Accepted

### Context
Offering a separate "search by media type" mode would duplicate UI and add modes, increasing complexity.

### Decision
Implement content-type (text/audio/photo) as a **filter applied on top of the existing tag/date/text search**, not as a separate search mode.

### Consequences
- ✅ One unified search surface; simpler, more consistent UI.
- ✅ Filters compose naturally.
- ⚠️ None significant.

---

## ADR-0008 — AI is optional and off the capture path

**Status:** Accepted

### Context
AI can add a lot of value (transcription, semantic search, tagging) but can also introduce latency, privacy concerns, and friction if placed carelessly.

### Decision
AI is **optional**, behind **provider-agnostic adapters**, and runs **only after capture** in the background. Capture and search must work identically with AI disabled. Cloud intelligence requires explicit opt-in.

### Consequences
- ✅ Capture budget and privacy are protected.
- ✅ Models are swappable; no vendor lock-in.
- ⚠️ Some intelligence is delayed until v3 and is opt-in.

---

## ADR-0009 — Monochrome, minimal design language

**Status:** Accepted

### Context
Nex must feel light and fast, like a capture surface — not like heavy productivity software. Rich theming and decoration risk cognitive load.

### Decision
Adopt a strict **black-and-white, minimal design language**: high contrast, generous whitespace, a single legible typeface, purposeful short motion, and color reserved for meaning only.

### Consequences
- ✅ Calm, fast, accessible (high contrast aids a11y).
- ✅ Consistent and easy to maintain.
- ⚠️ Less visual "personality" by choice — restraint *is* the personality.

---

## ADR-0010 — Soft delete over hard delete

**Status:** Accepted

### Context
Hard deletes break sync (a note deleted on one device can resurrect from another) and remove recoverability.

### Decision
Use **soft delete** (`deleted_at` tombstone) for all deletions. Deletions propagate via tombstones during sync and remain recoverable.

### Consequences
- ✅ Sync-safe deletions; no resurrected notes.
- ✅ Recoverability for users.
- ⚠️ Tombstones require eventual compaction/cleanup — a background concern, not a user-facing one.

---

## Decision-Making Heuristic

When facing a new choice, run it through the product's filter:

1. **Does it protect the 3-second capture?** If not, reject or rework.
2. **Does it preserve local-first and offline?** If not, justify heavily.
3. **Does it add a decision at capture time?** If yes, reject.
4. **Is it learnable in under 30 seconds?** If not, simplify.
5. **Does it reinforce "inbox, not system"?** If it pushes toward a second-brain platform, defer.

If a proposal fails this filter, the answer is **no** — regardless of how interesting the feature is.

---

> Nex's decisions are easy to predict: **choose whatever keeps capture effortless and find instant.**
> 
