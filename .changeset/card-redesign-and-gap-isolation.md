---
"@drop-in/graffiti": minor
---

**Card redesign: padding on `.card` itself, `.card-body` removed.**

`.card` is now the padded surface — drop content directly inside without a `.card-body` wrapper. Direct `<header>`, `<footer>`, `<img>`, `<picture>`, and `<figure>` children bleed edge-to-edge through the card's padding via negative margins, so the divided-bar and edge-to-edge media patterns still work without extra markup. Children stack vertically with `gap: var(--gap)` (default `var(--vs-s)`), overridable inline.

The old `.card-body` selector is gone. Migration:

```html
<!-- before -->
<article class="card">
  <div class="card-body stack">
    <p>…</p>
  </div>
</article>

<!-- after -->
<article class="card">
  <p>…</p>
</article>
```

Header/footer/media variants are unchanged at the markup level — drop them directly as children of `.card`.

**`--gap` is now registered as a non-inheriting `@property`.**

Previously, setting `--gap` on a parent `.stack` would cascade into every nested `.card`, `.cluster`, or other component that read `var(--gap, …)`, producing surprising spacing. `--gap` is now registered with `inherits: false`, so each component falls back to its own designed default and only the element you set it on uses the override.

`.cluster` and `.card` set their own `--gap` defaults explicitly (`0.5rem` and `var(--vs-s)` respectively). Inline overrides via `style="--gap: …"` work the same as before, but no longer leak into descendants.

If you were relying on a parent's `--gap` cascading into a nested component, set `--gap` directly on that component instead.
