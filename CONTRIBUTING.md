# Contributing to Nex

> Thanks for helping make capture effortless. Nex is built in the open, and good contributions are welcome — especially ones that make capture **faster** or the surface **simpler**.

**Status:** Authoritative · **Owner:** Maintainers · **Last updated:** 2026

---

## Before You Contribute

Nex has a strict identity. Before investing time in a change, confirm it fits:

- Nex is a **personal capture tool** and an **inbox for the mind** — not a knowledge-management, project-management, or second-brain platform.
- The mission is non-negotiable: **Capture First. Organize Later. Find Instantly.**
- **If a change adds friction to capture, adds decisions at capture time, or complicates the UI, it will not be accepted** — even if it is technically excellent.

Read these first:

- [01 — Product Vision](./01-product-vision.md) (especially *Non-Negotiable Principles*)
- [02 — Product Specification](./02-product-specification.md) (*MVP Scope*, *Non-Goals*)
- [10 — Decisions](./10-decisions.md) (why things are the way they are)

---

## Ways to Contribute

- 🐛 **Bug reports** — especially anything that risks **losing a capture** or **slowing capture/search**.
- ⚡ **Performance** — improvements to the capture path or search latency.
- 🎨 **Design/UX** — making the surface simpler, calmer, or more accessible.
- 📱 **Platform** — desktop/mobile packaging, offline edge cases.
- 🧪 **Tests** — especially around the repository, capture, and search.
- 📚 **Docs** — clarity, examples, and corrections.
- 🌍 **i18n/a11y** — translations and accessibility improvements.

**Not sought right now:** scope-expanding features (transcription, sync internals, generic files, semantic search) are version-gated (see [08 — Roadmap](./08-roadmap.md)) and tracked by maintainers.

---

## Getting Started

1. **Fork & clone** the repository.
2. **Install dependencies** (see [03 — README](./03-readme.md) for the recommended stack).
3. **Create a branch** named by intent: `feat/text-capture`, `fix/search-date`, `docs/readme`.
4. **Run the app locally** and confirm you can capture a note end-to-end.
5. **Make your change**, keeping it small and focused.
6. **Test** against the criteria below.
7. **Open a Pull Request** against `main`.

---

## Coding Standards

- Follow [06 — Development Guide](./06-development.md): layered modules, local-first, no network on the capture path.
- **Type-safe** end to end; the domain layer is framework-free.
- **Naming** per the conventions in the dev guide.
- **No new heavy dependencies** without justification — a small footprint is a feature.
- **Accessibility by default:** keyboard-reachable, AA contrast, reduced-motion friendly (see [05 — Design](./05-design.md)).
- **Commits** use [conventional commits](./06-development.md#git-workflow): `feat:`, `fix:`, `perf:`, `refactor:`, `test:`, `docs:`, `chore:`.

---

## Pull Request Checklist

A maintainer will look for all of these:

- [ ] **No added capture friction** — the capture path stays under 3 s, offline.
- [ ] **Local-first preserved** — no new hard dependency on the network.
- [ ] **Tests added/updated** for the behavior you changed.
- [ ] **Performance budgets met** (capture < 3 s, search < 200 ms).
- [ ] **Accessibility maintained** (keyboard, contrast, reduced-motion).
- [ ] **Docs updated** if behavior or architecture changed.
- [ ] **Fits scope** — does not expand v1 scope into v2/v3 territory.

> If your PR adds a Save button, a required title, a folder hierarchy, or a network call to capture — it will be declined. These are product principles, not preferences.

---

## Reporting Bugs

Open an issue with:

- **Summary** — what happened vs. what you expected.
- **Steps to reproduce** — minimal and exact.
- **Impact** — did it risk losing a capture or slowing capture/search?
- **Environment** — OS, app version, online/offline.
- **Logs** — from the in-app debug toggle (**never** paste private note content).

**Security or data-loss bugs:** do **not** open a public issue. Email the maintainers privately.

---

## Code of Conduct

Be kind, respectful, and constructive. Harassment, discrimination, and personal attacks are not tolerated. Assume good intent, give clear feedback, and remember that everyone here is volunteering time toward the same goal: **the fastest, lightest capture tool.**

---

## Recognition

Contributors are credited in release notes. Exceptional contributions to capture speed, reliability, or simplicity may be highlighted in the project's changelog.

---

> The best contribution to Nex is one that **removes a step between an idea and its capture.**
