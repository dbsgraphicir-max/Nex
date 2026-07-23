# Nex — Design System

> Companion to [`Nex Product Vision`](./01-nex-product-vision.md#ux-philosophy). This document defines the visual and interaction language that makes Nex feel "light" rather than like software.

---

## Design Language

Nex's visual identity is **minimal, monochrome, and quiet**. The interface should never compete for attention with the user's thought — it should disappear around it.

Guiding statement: *if a design element doesn't help the user capture or find something faster, remove it.*

- Black and white as the primary palette; no decorative color.
- Generous white space; content is never cramped against edges or against other content.
- Highly legible typography at every size.
- Short, purposeful motion — never decorative, never delayed.
- No skeuomorphism, no gradients-as-decoration, no illustrations that don't carry information.

---

## UI Principles

1. **One primary action per screen.** The Timeline's primary action is "+". The Capture screen's primary action is "provide content." Nothing competes with it visually.
2. **No modal interrogations.** Dialogs that ask the user to decide something before they can proceed (name it, file it, choose a type beyond the initial three) are disallowed by design policy.
3. **Progressive disclosure.** Tags, timestamps, and metadata are visible but never demand interaction — they're available when wanted, invisible when not.
4. **Consistent, predictable placement.** The "+" action and the Search entry point occupy fixed, muscle-memory positions across the Timeline at all times.
5. **Content is the interface.** Cards show the user's own words, recordings, and photos — not decorative chrome.
6. **Every screen must be understood in under 30 seconds** with zero onboarding, consistent with the [non-negotiable principles](./01-nex-product-vision.md#non-negotiable-principles).

---

## Typography

- A single, highly legible sans-serif typeface family is used throughout the product (e.g., a system-native font such as Inter, SF Pro, or Segoe UI, depending on platform) to keep footprint low and rendering native-feeling.
- Type scale is restrained and used consistently:

| Role | Example Use | Weight |
|---|---|---|
| Display | Onboarding/empty states only | Semibold |
| Title | Note detail heading, section headers | Semibold |
| Body | Note content, capture input | Regular |
| Caption | Timestamps, tag chips, metadata | Regular / Medium |

- Line height is generous (1.4–1.6x) to preserve the "light" feeling and support long-form text capture readability.
- No more than two font weights are used on a single screen at once.

---

## Color Philosophy

Nex is intentionally black-and-white first:

| Token | Light Mode | Dark Mode | Usage |
|---|---|---|---|
| `bg-primary` | `#FFFFFF` | `#0A0A0A` | App background |
| `bg-elevated` | `#F5F5F5` | `#171717` | Cards, sheets |
| `text-primary` | `#0A0A0A` | `#FAFAFA` | Primary text/content |
| `text-secondary` | `#6B6B6B` | `#A3A3A3` | Timestamps, metadata, captions |
| `border` | `#E5E5E5` | `#262626` | Dividers, card outlines |
| `accent` | `#0A0A0A` (inverted per mode) | `#FAFAFA` | The "+" action, active states — never a "brand color," always the inverse of the background |

- **No accent color palette.** Nex does not use color to signal priority, category, or brand — color would introduce a decision ("what does red mean here?") that contradicts Capture First.
- **Tags are visually neutral** — rendered as simple bordered chips in `text-secondary`/`border` tones, never color-coded, so that tag color never becomes an implicit categorization system users have to maintain.
- **Dark mode is a first-class, symmetric palette**, not an inverted afterthought — since capture often happens in low-light, at night, or first thing in the morning.
- The **only** deliberate use of stronger visual weight is the "+" capture action and active/recording states (e.g., a pulsing indicator during voice capture) — because those are the one thing the interface should never let the user miss.

---

## Components

Core component set for the MVP surface:

| Component | Purpose | Design Notes |
<br/>
|---|---|---|
| **Capture Button (+)** | Universal entry point to text/voice/photo capture | Always visible on the Timeline, fixed position, largest single interactive element on screen |
| **Capture Sheet** | Presents the three capture types | Appears instantly (no loading state), dismissible by outside tap |
| **Timeline Card** | Represents one note in the stream | Adapts preview to content type (text snippet / waveform + duration / photo thumbnail); shows relative timestamp and tag chips if present |
| **Tag Chip** | Represents a single tag | Neutral color, rounded, removable via inline "×" in edit contexts |
| **Search Bar** | Entry point + live query field | Always paired with filter affordances (tag / date / type) that expand without navigating away |
| **Filter Control** | Tag / date / content-type filters | Presented as simple toggles/pills, combinable, always reversible with a single "clear" action |
| **Note Detail Sheet** | Expanded view of a single note, tag editing | Opens as a lightweight overlay, not a full context switch, to preserve the feeling of staying in the Timeline |
| **Voice Recorder Bar** | Active recording state | Shows a live waveform and elapsed time; the stop action is the single largest control on screen |
| **Empty State** | Shown only when the Timeline has zero notes | A single, quiet prompt pointing at the "+" button — never a tutorial carousel |

---

## Icons

- A single, consistent icon set (line-style, uniform stroke width) is used throughout — no mixing of filled and outlined icon families.
- Icons are used only where they communicate faster than text (capture types, play/stop, search, filters) — never as decoration.
- Every icon-only control has an accessible label (see [Accessibility](#accessibility)).

---

## Animations

Animation exists only to **confirm**, never to **delight for its own sake**.

- **Duration:** 120–200ms for micro-interactions (button press, chip add/remove); 200–300ms for sheet transitions (Capture Sheet open/close, Note Detail open/close).
- **Easing:** standard ease-out for entrances, ease-in for exits — consistent across the whole app rather than per-component bespoke curves.
- **Purposeful motion only:**
  - Capture Sheet slides/fades in to confirm it's ready for input.
  - A saved note animates briefly into position at the top of the Timeline to confirm "it's there."
  - Voice recording uses a live waveform as continuous, functional (not decorative) motion.
- **No motion that delays interaction.** Nothing animates *before* becoming interactive; the user is never left waiting on a flourish.
- **Respect reduced-motion settings** at the OS level — when enabled, all non-essential transitions are replaced with instant state changes.

---

## Accessibility

Accessibility is treated as core functionality, not a compliance checkbox — a slow or confusing experience for any user contradicts Nex's core promise.

- **Contrast:** All text/background combinations meet WCAG 2.1 AA contrast ratios (4.5:1 for body text, 3:1 for large text), in both light and dark palettes.
- **Tap targets:** Minimum 44×44pt touch targets for all interactive elements, most critically the "+" capture action and the voice stop control.
- **Screen reader support:** Every icon-only control (capture types, play/stop, filters) has a descriptive accessible label; Timeline cards announce content type, a text preview or transcription placeholder, timestamp, and tags in a single coherent read-out.
- **Dynamic type:** UI text scales with system font-size settings without breaking layout or truncating capture input.
- **Voice capture alternative:** Text and photo capture remain full alternatives to voice capture for users who cannot or prefer not to use audio input.
- **Motion sensitivity:** All animation respects the OS-level "reduce motion" preference, as noted above.
- **Color independence:** No information is conveyed by color alone (consistent with the monochrome palette by construction).
