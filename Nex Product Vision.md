# Nex — Product Vision

> Capture in Seconds. Find in Seconds.

**Status:** Living document · **Owner:** Product & Design · **Last updated:** 2026

---

## Executive Summary

Nex is a personal capture tool built around a single conviction: **the friction of capturing an idea is usually greater than the friction of forgetting it.**

Most note-taking apps force you to open the app, create a note, give it a title, pick a folder, and press **Save**. By the time those steps are done, the idea is often gone. Nex removes that friction. It is the **inbox for the human mind** — a place to drop anything in under three seconds, before it disappears, and to find it again in under three seconds when it matters.

Nex is deliberately **not** a knowledge management system, a project management tool, or a second-brain platform. It is the **doorway** to a second brain: the fastest possible place to capture a thought, leaving organization for later.

---

## Why Nex Exists

Capturing is harder than forgetting.

To record an idea today you typically have to open an app, create a new note, type a title, choose a folder, and press **Save**. That handful of seconds of friction causes many ideas to never be recorded at all.

**Quick Capture** exists to eliminate this friction.

> Capture anything in under 3 seconds. Find anything in under 3 seconds.

The core problem Nex solves is **the scattering and loss of ideas**. Every missed capture is a lost thought. Every thought that cannot be found later is effectively lost too. Nex attacks both ends: zero-friction capture and instant retrieval.

---

## Mission

> **Capture First. Organize Later. Find Instantly.**

Nex exists to make capturing a thought faster than thinking about it, and finding that thought faster than searching for it.

---

## Vision

A world where **no idea is ever lost to friction**.

Nex aims to be the fastest, lightest, most obvious place to capture anything — on any device, offline or online — so that the gap between *having* an idea and *keeping* it disappears. Organization, intelligence, and cross-device sync are layered on later, never in the way of the moment of capture.

---

## Product Identity

**Nex is:**

- A personal capture tool
- An inbox for the human mind
- Local-first
- Offline-first
- Minimal
- Fast
- AI-optional

**Nex is NOT:**

- A knowledge management system
- A project management tool
- A second-brain platform
- Another Notion
- Another Obsidian
- Another Evernote

Every product, design, and engineering decision must reinforce this identity. When in doubt, Nex chooses the option that makes capture faster and the surface simpler.

---

## Target Users

Nex is for **anyone who loses ideas to friction**. Primary personas:

| Persona | Motivation | How they use Nex |
| --- | --- | --- |
| **The Idea Hoarder** | Has ideas constantly, hates losing them | Text capture on desktop; audio on mobile |
| **The Mobile-First Thinker** | Best ideas arrive on the move | One-tap audio and photo capture |
| **The Cross-Device Worker** | Lives across phone, laptop, desktop | Timeline + (future) seamless sync |
| **The Minimalist** | Hates cluttered, heavy tools | A timeline and a single big `+` button |
| **The Student / Learner** | Captures concepts, links, reminders | Optional tags to group related notes |

Nex is **personal**. v1 is a single-user product. Multi-user, sharing, and collaboration are explicitly out of scope.

---

## Core Values

1. **Speed over features.** If a feature slows down capture, it does not belong in Nex.
2. **Simplicity over power.** Fewer concepts, learned in seconds.
3. **Trust through reliability.** A captured note must never be lost.
4. **Honesty in the UI.** Show limitations plainly rather than hiding them.
5. **Restraint.** Say no to feature creep. The identity is "capture first."

---

## Design Philosophy

Three principles drive every design decision:

### 1. Capture First
Capturing must be faster than thinking. While capturing, the user must make **no decisions**: no folder, no format, no Save button. Everything flows into a single timeline. Organization — tags, grouping — happens later, optionally.

### 2. One Inbox
All captured items live in one time-ordered timeline. No default folders, no required categorization. The timeline is the home.

### 3. Find Instantly
If you cannot find something, capturing it was worthless. Search is the second pillar of the product, equal in importance to capture.

---

## UX Philosophy

- **Zero friction.** The path from idea to stored note must be the shortest physically possible.
- **No mandatory title.** No mandatory folder. No Save button.
- **Learnable in under 30 seconds.** Every feature must be discoverable and obvious.
- **Lightness.** The interface should feel weightless — not like project-management software.
- **Short animations.** Motion is used sparingly to confirm actions, never to entertain.
- **Generous whitespace and a readable typeface.** Calm, focused, uncluttered.

---

## Non-Negotiable Principles

Treat these as hard constraints.

- Capture takes **less than 3 seconds**.
- Finding information takes **less than 3 seconds**.
- **Zero friction.**
- **No mandatory title.**
- **No mandatory folder.**
- **No Save button.**
- **Timeline is the default home.**
- **Organize later.**
- **AI never interrupts capture.**
- **Local-first architecture.**
- **Cloud sync is optional.**
- **Every feature must be learnable in under 30 seconds.**
- **If a feature slows down capture, it does not belong in Nex.**

---

## Success Metrics

Because Nex is local-first and privacy-respecting, metrics emphasize behavior and reliability over engagement hacking.

| Metric | Target | Why it matters |
| --- | --- | --- |
| **Capture latency** | < 3 s from app-open to stored note | Core promise |
| **Time-to-first-capture** | < 30 s for a brand-new user | Zero onboarding friction |
| **Search latency** | < 200 ms local query | "Find instantly" |
| **Capture reliability** | 99.99% of captures persisted before UI feedback | Trust: nothing lost |
| **Sync success (v2+)** | > 99.9% of changes converge across devices | Cross-device coherence |
| **7-day retention** | Trending up cohort-over-cohort | Product solves a real need |
| **Feature discoverability** | Core features found within 30 s in usability tests | Learnability promise |

We do **not** optimize for time-in-app. Nex is designed to be opened quickly and closed quickly.

---

## Product Boundaries

**In scope for v1 (MVP):**

- A single time-ordered timeline
- Quick Capture of three types: **text**, **audio**, **photo**
- Auto-save, no Save button, return straight to timeline
- Search by text, tag, and date, with a content-type filter
- Tags as the **only** organization tool (optional)
- Local-first storage with sync-ready architecture

**Explicitly out of scope for v1:**

- Speech-to-text / transcription (planned for v3)
- Related Notes
- Export
- Generic "file" capture (fourth capture type, planned for v2)
- Complex organization (notebooks, hierarchies, links)
- Real-time multi-device sync (architecture-ready in v1, active in v2)

---

## AI Philosophy

**AI is optional and never in the way.**

Nex's AI exists only to *assist after capture* — never to interrupt, gate, or slow the moment of capture. In v1, there is no AI in the capture loop at all.

Where AI may help later:

- Auto-tagging suggestions (opt-in)
- Semantic search (complementing keyword search)
- Summarization
- Transcription of audio (v3)
- OCR of photos (future)
- Related Notes (future)

Guiding rule: **AI is a layer above capture, never a gate in front of it.**

---

## Long-Term Vision

Nex's roadmap protects the capture experience while growing capabilities around it:

- **v1** — The fastest capture experience. Timeline + text/audio/photo + tags + instant local search.
- **v2** — Seamless cross-device sync (Android, Windows, iOS) as the headline feature; generic file capture.
- **v3** — Intelligence: transcription makes audio text-searchable, plus semantic search, OCR, tag suggestions, and summarization.

Throughout, Nex stays the **doorway**, not the destination. It is the inbox for a second brain, never the second brain itself.

---

> *Capture it — before you forget it.*
> *Capture in Seconds. Find in Seconds.*
