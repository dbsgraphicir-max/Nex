# Contributing to Nex

Thank you for considering a contribution to Nex. This document explains how to propose changes and, just as importantly, what kinds of changes fit the project.

---

## Before You Contribute

Nex has a narrow, deliberate identity. Please read these first:

- [`Nex Product Vision`](./01-nex-product-vision.md) — especially [Non-Negotiable Principles](./01-nex-product-vision.md#non-negotiable-principles)
- [`Nex Product Specification`](./02-nex-product-specification.md) — current scope and explicit non-goals

**The single most common reason a pull request is rejected is that it adds friction to capture, even if the code is technically excellent.** If you're unsure whether a feature belongs, open a discussion issue before writing code.

---

## Ways to Contribute

- **Bug fixes** — always welcome, especially anything affecting capture reliability, offline behavior, or search correctness.
- **Performance improvements** — especially to capture-to-save and query-to-result latency.
- **Accessibility improvements** — see [`DESIGN.md`](./05-design.md#accessibility).
- **Documentation improvements** — clarifications, corrections, translations.
- **Roadmap features** — see [`ROADMAP.md`](./08-roadmap.md); features already scoped for an upcoming version are the best place to start.
- **New feature proposals** — must go through a Discussion/Issue first (see below) before a PR, since anything not already on the roadmap needs an identity check against the product's non-negotiable principles.

## What We Will Not Merge

- Anything that adds a required field, dialog, or decision point to the capture flow (title, folder, template, confirmation prompts).
- Anything that turns Nex into a general-purpose knowledge base, project manager, or collaboration tool (see [Product Boundaries](./01-nex-product-vision.md#product-boundaries)).
- Features that make AI a blocking step in capture (see [`AI.md`](./09-ai.md)).
- Dependencies that meaningfully increase app size or cold-start time without a corresponding, justified capability the product actually needs today.
- Speculative abstractions/config systems for functionality that isn't on the current roadmap.

---

## Development Setup

See [`DEVELOPMENT.md`](./06-development.md) for folder structure, conventions, and testing strategy. In short:

```bash
git clone https://github.com/<org>/nex.git
cd nex
npm install
npm run test --workspace=packages/core
```

---

## Proposing a Change

1. **Search existing issues** to avoid duplicates.
2. **For anything beyond a small fix, open an issue first** describing the problem, the proposed solution, and — critically — how it aligns with Nex's identity and non-negotiable principles.
3. **Wait for maintainer feedback** on scope before investing significant implementation time. This protects your time as much as the project's coherence.

---

## Pull Request Process

1. Fork the repository and create a branch following the convention in [`DEVELOPMENT.md`](./06-development.md#naming-conventions): `type/short-description`.
2. Write tests for any new logic, prioritizing Core domain and Data layer coverage as described in the [Testing Strategy](./06-development.md#testing-strategy).
3. Ensure the full CI suite passes locally before opening the PR: lint, type-check, unit/integration tests, and performance budget checks.
4. Fill out the PR template, explicitly answering:
   - What problem does this solve?
   - Does this change the capture flow? If yes, what is the measured impact on capture time?
   - Does this change align with a specific principle in the Vision or Specification docs?
5. Keep PRs focused and small. Large, multi-concern PRs will be asked to split.
6. At least one maintainer approval and a green CI run are required before merge.
7. Maintainers squash-merge using a Conventional Commits-formatted message.

---

## Code Review Standards

Reviewers evaluate PRs against, in order:

1. **Does it preserve the < 3 second capture and find guarantees?**
2. **Does it preserve offline-first behavior?**
3. **Does it avoid adding any decision point to the capture flow?**
4. **Is it well-tested per the [Testing Strategy](./06-development.md#testing-strategy)?**
5. **Is it consistent with existing conventions and design language ([`DESIGN.md`](./05-design.md))?**

---

## Reporting Bugs

Please include:
- Platform and version (Android/Windows/iOS, app version).
- Steps to reproduce.
- Expected vs. actual behavior.
- Whether the issue affects capture, search, sync, or another area.
- Logs, if available — never include actual note content in a public bug report, since Nex treats note content as private by default (see [`AI.md`](./09-ai.md) and [Logging](./06-development.md#logging)).

---

## Proposing New Features

Open a "Feature Proposal" discussion including:
- The problem being solved, from a real user scenario.
- Why existing capture/search/tag primitives don't already solve it.
- An explicit statement of how the feature preserves Capture First, Organize Later, and Find Instantly.
- Any UX decisions it would introduce at capture time (if none, say so explicitly — this is often the deciding factor).

Feature proposals that are accepted are added to [`ROADMAP.md`](./08-roadmap.md) with a target version before implementation begins.

---

## Community Standards

- Be respectful and constructive in issues, discussions, and reviews.
- Assume good faith; the project's narrow scope means many well-intentioned ideas will still be declined — that's a reflection of focus, not of the idea's merit elsewhere.
- All contributors are expected to follow a standard open-source Code of Conduct (Contributor Covenant v2.1), enforced by maintainers.

---

## License

By contributing, you agree that your contributions will be licensed under the project's [MIT License](./LICENSE).
