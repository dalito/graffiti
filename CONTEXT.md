# Graffiti

Graffiti is a CSS theming and primitives package: design tokens, fluid typography, layout primitives, utilities, and component patterns. It is consumed both as an NPM import and as a CLI that copies `drop-in.css` into a project.

## Language

**Token**:
A CSS custom property declared on `:root` or another scoping element. Tokens carry meaning the framework or a consumer can override.
_Avoid_: variable, custom property (use these only when speaking strictly about the CSS feature, not Graffiti's design system).

**Literal token**:
A token whose value is a concrete primitive — a color, a length, a duration. Examples: `--blue`, `--pad-l`, `--vs-base`, `--lh-s`. Literals are the source colors and spacings the rest of the system composes from.

**Semantic token**:
A token whose value resolves through one or more literals to express *purpose*. Examples: `--primary`, `--accent`, `--focus-ring`, `--border-1`, `--shadow-2`. Semantic tokens are what components should consume; literals are what consumers may override at the root.

**Alpha scale**:
A nine-step color scale built by varying *alpha*, not lightness — e.g. `--blue-1` (10% alpha of `--blue`) through `--blue-9` (full opacity). Designed for tints, overlays, and surfaces that should adapt to the underlying background and `color-scheme`.
_Avoid_: lightness scale, opacity scale (`opacity` is a property; alpha is a channel — they're not the same).

**Layout primitive**:
A class in `@layer layouts` that establishes structural frame and responsive behavior. Examples: `.layout-sidebar`, `.layout-card`, `.layout-readable`, `.layout-holy-grail`, `.stack`, `.cluster`, `.carousel`, `.reel`. Layout primitives are the outermost shapes a page is built from; their breakpoint behavior is part of the contract.

**Utility**:
A class in `@layer utilities` that toggles a single property or a tightly coupled pair. Examples: `.flex`, `.grid`, `.split`, `.text-center`, `.full`, `.transition`, `.aspect-square`. Utilities are atomic and may be applied inside any layout, but cannot override a layout primitive's structural decisions (see [ADR 0002](./docs/adr/0002-cascade-layer-order.md)).

**Component**:
A class in `@layer components` that ships a finished visual pattern — surface, padding, border, motion. Examples: `.card`, `.feature-card`, `.stat-card`, `.toc`, `.newsletter`. Components consume semantic tokens; consumers customise components by overriding tokens, not by overriding component rules.

**Fluid level (`--fl`)**:
A scalar (typically `-1` through `6`) that selects a step on Graffiti's modular type scale. Setting `--fl: 3` on any element resizes its text to that step, scaled fluidly between viewport breakpoints.

## Relationships

- A **literal token** may feed one or more **semantic tokens** (`--blue` → `--primary`).
- A **component** consumes **semantic tokens**, never **literal tokens** directly.
- A **layout primitive** wins over a **utility** applied within it ([ADR 0002](./docs/adr/0002-cascade-layer-order.md)).
- A **utility** wins over a **component** for atomic property toggles.

## Flagged ambiguities

- **"Alpha scale" vs a future "lightness scale"**: today, `--{color}-1`…`--{color}-9` is alpha-based. There is an open question about adding a parallel non-alpha scale (built via `color-mix()` with `bg`/`fg`) for cases where alpha-on-background isn't sufficient — e.g. opaque text-tier tints. If introduced, naming must clearly distinguish the two scales to avoid the Tailwind/Radix mental-model clash.
- **"Layout" historically overlapped with "utility"** for classes that set `display: flex/grid` (`.flex`, `.split`, `.cluster`, `.grid`). These remain utilities by classification because they're atomic, but the cascade order is now set so a layout primitive can still override them on a child element.
