# Nex — Product Vision

> **Capture in Seconds. Find in Seconds.**

---

## Executive Summary

Nex is a personal capture tool designed to eliminate the friction between having a thought and recording it. It is not a note-taking app, not a knowledge base, and not a project manager — it is the **inbox of the human mind**.

The product exists to solve one very specific, very human problem: **ideas die between the moment they occur and the moment we get around to writing them down.** Every additional decision a capture tool demands — pick a folder, choose a template, name the note, hit save — is a chance for the thought to evaporate.

Nex removes all of that. One tap, one thought, done. Organization, tagging, and structure are deliberately deferred to "later," because "later" is optional, but "now" is not.

---

## Why Nex Exists

Most note-taking and knowledge-management tools were designed to organize information *well*, not to capture it *fast*. They optimize for the 5% of notes that become permanent knowledge and, in doing so, punish the 95% of fleeting thoughts that never survive the friction of entry.

The result is a predictable failure mode:

1. A thought occurs.
2. The user hesitates — "Where should this go?"
3. The user opens an app that asks too many questions before it lets them type.
4. The thought is gone, or the user gives up and uses a worse tool (a chat message to themselves, a sticky note, nothing at all).

Nex exists to interrupt this failure mode at step 2. **There is no "where." There is only "now."**

---

## Mission

> Make capturing any thought — text, voice, or image — faster than the act of forgetting it.

---

## Vision

Nex becomes the universal, frictionless front door to every other tool a person uses to think, plan, and organize. It does not compete with Notion, Obsidian, or Evernote — it feeds them. Every idea, reminder, voice memo, and snapshot enters life through Nex first; what happens to it afterward is up to the user and, eventually, up to other tools that consume Nex's data.

In five years, "just Nex it" should be the default reflex for capturing a thought, the way "just Google it" became the default reflex for a question.

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
- A "second brain" platform
- Another Notion
- Another Obsidian
- Another Evernote

Every roadmap decision, every feature request, and every design review must be checked against this identity. If a proposed feature makes Nex look more like a knowledge base or a project tool, it does not belong in Nex — regardless of how useful it might be in isolation.

---

## Target Users

| Persona | Description | Primary Need |
|---|---|---|
| **The Idea Hoarder** | Has constant bursts of ideas (product, creative, business) throughout the day | Capture before the idea disappears |
| **The Multitasker** | Switches between devices and contexts (desk, commute, meetings) | A single, always-available capture surface |
| **The Voice-First Thinker** | Thinks out loud, prefers speaking over typing | Instant voice recording with zero setup |
| **The Visual Note-Taker** | Captures whiteboards, receipts, screens, physical documents | One-tap photo capture |
| **The Overwhelmed Organizer** | Has tried Notion/Obsidian but abandoned them because setup felt like a chore | A tool that asks nothing up front |

All personas share one trait: they have been let down by tools that make capture feel like work.

---

## Core Values

1. **Speed over structure.** A fast, unorganized capture beats a slow, perfectly organized one.
2. **Zero decisions at capture time.** Every prompt, dialog, or required field is a tax on memory.
3. **Trust through simplicity.** Users must never wonder "did that save?" — it always does, silently.
4. **Respect for attention.** Nex should feel invisible until needed, not a place users "spend time in."
5. **Data belongs to the user.** Local-first by default; sync and cloud features are additive, never mandatory.

---

## Design Philosophy

Three principles govern every design decision in Nex.

### Capture First
Capturing must be faster than thinking. At the moment of capture, the user makes **zero** decisions: no folder, no template, no save button. Just capture.

### Organize Later
Everything lands in a single, unified timeline first. Tagging and categorization are optional actions the user can take *after* the fact, never a precondition for saving.

### Find Instantly
A capture tool nobody can search is worthless. Search is the second pillar of the product, on equal footing with capture itself.

---

## UX Philosophy

- The interface should feel like a **blank page waiting for you**, not a form to fill out.
- Every screen should be understandable in under 30 seconds, with no onboarding tour required.
- Motion should be brief and purposeful — confirming an action, never decorating it.
- The product should feel "light," like a notepad in your pocket — never like enterprise software.
- Silence is a feature: no notifications, no gamification, no engagement loops. Nex is a tool, not a habit-forming app.

---

## Non-Negotiable Principles

These constraints apply to every version of Nex, forever, regardless of feature additions:

- Capture takes less than 3 seconds.
- Finding information takes less than 3 seconds.
- Zero friction at the moment of capture.
- No mandatory title.
- No mandatory folder.
- No Save button — saving is automatic and invisible.
- The Timeline is the default home screen.
- Organization always happens later, never at capture time.
- AI never interrupts or delays capture.
- The architecture is local-first.
- Cloud sync is optional, never required for core functionality.
- Every feature must be learnable in under 30 seconds.
- If a feature slows down capture, it does not belong in Nex.

---

## Success Metrics

Nex's success is measured by capture behavior and retrieval confidence, not by "engagement" in the conventional sense.

| Metric | Target | Why It Matters |
|---|---|---|
| Time-to-first-capture (new user) | < 10 seconds from install | Validates zero-friction onboarding |
| Median capture duration | < 3 seconds | Core product promise |
| Median search-to-result duration | < 3 seconds | Core product promise |
| Day-30 capture retention | High relative to category norms | Confirms Nex replaces the user's default capture habit |
| % of captures with no tag/title added | Expected to be high (60–80%) | Confirms "capture first" is actually happening, not just claimed |
| Search success rate | > 90% of searches result in a click/open | Confirms retrieval is trustworthy |
| Crash-free capture sessions | > 99.9% | Trust is the product; a lost capture is a broken promise |

Metrics that Nex explicitly does **not** optimize for: daily session count, time spent in app, streaks, or notification open rate. Maximizing "time in app" directly contradicts the product's mission.

---

## Product Boundaries

Nex deliberately stays out of:

- Rich document editing (no nested pages, no databases, no complex formatting)
- Project/task management (no deadlines, no assignees, no boards)
- Team collaboration (Nex is single-player by design in its first versions)
- Being a destination for long-term structured knowledge work

Nex is the **front door**, not the house.

---

## AI Philosophy

AI is a tool that removes friction *after* capture — never a gatekeeper *during* capture.

- AI is entirely optional and can be disabled without any loss of core functionality.
- AI never blocks, delays, or requires confirmation during the capture flow.
- AI assists with tagging, transcription, OCR, semantic search, summarization, and surfacing related notes — always after the fact, always in the background.
- AI suggestions are always dismissible and never silently alter the user's original content.

See [`AI.md`](./09-ai.md) for the full strategy.

---

## Long-Term Vision

1. **Year 1:** Establish Nex as the fastest capture tool available on mobile and desktop, with a rock-solid timeline and search experience.
2. **Year 2:** Make capture ubiquitous across devices through real, reliable sync — without ever compromising local-first guarantees or offline reliability.
3. **Year 3+:** Layer intelligence on top of the capture graph — transcription, OCR, semantic search, and summarization — so that everything ever captured becomes effortlessly retrievable, no matter its original format.
4. **Beyond:** Nex becomes interoperable — an open inbox that can hand off captures to the knowledge tools of the user's choice (Notion, Obsidian, plain markdown export, etc.), fulfilling its role as the entry point to a personal "second brain" ecosystem without ever trying to become one itself.

Throughout every stage, the mission does not change:

> **Capture First. Organize Later. Find Instantly.**
