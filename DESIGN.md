# Nex — Design

> Minimal. Black and white. Fast. Light. Calm.

**Status:** Authoritative · **Owner:** Design · **Last updated:** 2026

Nex's interface must feel **weightless** — like a fast capture surface, never like project-management software. Every visual decision reinforces a single feeling: *this is the fastest place to drop a thought.*

---

## Design Language

- **Minimal and monochrome.** A strict black-on-white (and white-on-black, in dark mode) system. Color is reserved for meaning (state), never decoration.
- **Content-first.** The user's words and captures are the focus; chrome recedes.
- **Generous whitespace.** Breathing room signals calm and reduces cognitive load.
- **High contrast, high legibility.** A readable typeface at comfortable sizes.
- **Short, purposeful motion.** Animation confirms an action; it never entertains or delays.

The guiding emotion: **lightness and immediacy.**

---

## UI Principles

1. **One tap to capture.** The `+` button is always reachable and obviously the primary action.
2. **Zero decisions at capture.** No title field, no folder picker, no Save button. Decisions belong to "later."
3. **Timeline is home.** The default surface is the single chronological stream.
4. **Progressive disclosure.** Show the essentials; reveal tags, filters, and detail on demand.
5. **Honest affordances.** If something has a limitation (e.g., audio is tag/date-only searchable), show it plainly.
6. **Forgiving.** Auto-save everything; make destructive actions recoverable.
7. **Consistency.** The same patterns everywhere — one way to capture, one way to search, one card style.

---

## Typography

- **One type family**, chosen for legibility on small screens and at speed — a neutral humanist/grotesque sans-serif (e.g., Inter, or the platform system font).
- **Clear hierarchy** via size and weight, not color:
  - **Display/Title** — large, semibold (timeline header, empty states).
  - **Body** — regular, comfortable size for note content.
  - **Meta** — small, muted, for timestamps and helper text.
- **Monospace** is used sparingly — only for technical/data contexts (counts, debug), never for body content.
- **No decorative fonts.** Restraint is the aesthetic.

| Role | Weight | Use |
| --- | --- | --- |
| Display | 600 | Headers, hero text |
| Body | 400 | Note content, primary text |
| Body Strong | 600 | Selected/active states |
| Caption | 400 | Timestamps, helper/limit text |

---

## Color Philosophy

Nex is **deliberately monochrome**. Color is a signal of meaning, never of style.

- **Light theme:** pure white background (`#FFFFFF`), near-black ink (`#0A0A0A` / `#111111`), grayscale neutrals for borders and muted text.
- **Dark theme:** near-black background (`#0A0A0A`), near-white ink (`#F5F5F5`), matching grayscale neutrals.
- **Semantic accent (used sparingly):** a single reserved tone may indicate an active state or a limitation note. It is never decorative.
- **Grayscale ramp:** a small, fixed neutral scale (e.g., `gray-50 → gray-900`) for surfaces, borders, and muted text.

> Rule: **if a color is not conveying state or meaning, it should not exist.**

### Suggested neutral ramp (light)

| Token | Value | Use |
| --- | --- | --- |
| `bg` | `#FFFFFF` | App background |
| `surface` | `#FAFAFA` | Cards, inputs |
| `border` | `#E5E5E5` | Dividers, outlines |
| `muted` | `#737373` | Timestamps, helper text |
| `ink` | `#0A0A0A` | Primary text |

---

## Components

A small, consistent set — by design. Complexity in components is a smell.

| Component | Purpose | Notes |
| --- | --- | --- |
| **Capture Button (`+`)** | Start Quick Capture | Large, always reachable, the visual anchor |
| **Note Card** | One item in the timeline | Minimal: preview, type icon, time, optional tags |
| **Timeline** | The home list | Virtualized, newest-first |
| **Capture Sheet** | Text/audio/photo entry | Auto-save, no Save button, returns to timeline |
| **Search Bar** | Query + filter entry | Single surface for text, tag, date, type |
| **Filter Chips** | Tag / date / type filters | Applied on top of search |
| **Tag Pill** | Display/edit a tag | Optional, removable |
| **Note Detail** | Read/play a note | Light, focused |
| **Empty State** | First-run / no results | Encourages a single next action |
| **Toast/Indicator** | Save confirmation | Brief, non-blocking |

Each component is **stateless where possible**, theme-aware, and accessible by default.

---

## Icons

- **Monochrome line icons**, a single consistent set (e.g., a lightweight open-source icon family such as Lucide/Heroicons-style outlines).
- **Stroke-based**, matching the line weight of the type for visual harmony.
- **One icon per concept** — no duplicate metaphors.
- Icons reinforce **type**: a text glyph, a waveform for audio, a camera/image for photo.
- **No emoji as primary UI** (emoji may appear in marketing/docs only).

---

## Animations

Motion is **functional, brief, and never blocking**.

- **Duration:** 120–200 ms for micro-interactions; never long enough to feel like a wait.
- **Easing:** ease-out for entrances, ease-in for exits; standard, calm curves.
- **Purpose:** confirm an action (a note sliding into the timeline), reveal/hide a sheet, or indicate a filter change.
- **Constraints:**
  - Never delay capture or navigation.
  - Respect `prefers-reduced-motion`: disable non-essential animation.
  - No looping/ambient animation that draws attention away from content.

---

## Accessibility

Accessibility is a **baseline requirement**, not a nice-to-have — and it aligns perfectly with Nex's high-contrast, content-first aesthetic.

- **Contrast:** meet **WCAG AA** (target AAA where practical) in both themes.
- **Keyboard-first:** every action — capture, search, open, tag — reachable and operable by keyboard.
- **Screen-reader support:** semantic markup, descriptive labels, live regions for save confirmation.
- **Touch targets:** minimum 44 × 44 px; the `+` button is intentionally larger.
- **Focus visibility:** clear, high-contrast focus rings.
- **Motion:** honor `prefers-reduced-motion`.
- **Color independence:** never rely on color alone to convey meaning (icons + text labels accompany color).
- **Legible text:** resizable, with a minimum body size; no text in images.

> A calm, high-contrast, keyboard-friendly surface is not just inclusive — it is *faster*, which is Nex's whole point.

---

> Design's mission: **make the next capture feel effortless, and the next find feel instant.**
