<!--
  CanonicalFixture — the six surface types every aesthetic preset gets
  rendered against on /themes. Keep markup minimal and class-first; the
  point is identical structure across presets so token + selector-rule
  differences read as visual deltas, not markup deltas.
-->
<section class="canonical-fixture stack">
  <!-- Button cluster -->
  <div class="cluster">
    <button class="primary">Primary</button>
    <button>Default</button>
    <button class="ghost">Ghost</button>
    <button disabled>Disabled</button>
  </div>

  <!-- Card with action -->
  <article class="card">
    <header>
      <h3>Card title</h3>
    </header>
    <p>
      A short body of card content that establishes baseline body type,
      paragraph spacing, and how the surface responds to the active preset.
    </p>
    <footer>
      <button class="primary">Action</button>
    </footer>
  </article>

  <!-- Form -->
  <form class="stack" onsubmit={(e) => e.preventDefault()}>
    <label class="form-row">
      <span>Email</span>
      <input type="email" placeholder="you@example.com" />
    </label>
    <label class="form-row">
      <span>Plan</span>
      <select>
        <option>Free</option>
        <option>Pro</option>
        <option>Team</option>
      </select>
    </label>
    <label class="form-option-row">
      <input type="checkbox" />
      <span>I agree to the terms</span>
    </label>
    <div class="form-actions">
      <button type="submit" class="primary">Submit</button>
      <button type="button" class="ghost">Cancel</button>
    </div>
  </form>

  <!-- Inline dialog open so it always renders in the fixture -->
  <dialog open>
    <h4>Dialog title</h4>
    <p>A brief dialog body explaining what action is about to happen.</p>
    <div class="form-actions">
      <button class="primary">Confirm</button>
      <button class="ghost">Cancel</button>
    </div>
  </dialog>

  <!-- Blog excerpt — h1, h2, paragraph long enough for ::first-letter
       to be a visible test, and a blockquote. -->
  <article class="prose stack">
    <h1>The Quiet Geometry of Type</h1>
    <h2>Notes on rhythm, contrast, and the page</h2>
    <p>
      Typography is the negotiation between author and reader, mediated
      by every choice the designer makes about rhythm and contrast. A page
      that breathes is a page that has been edited — not only the words,
      but the spaces between them, the weight of the headings, and the
      restraint at the corners. Good type asks nothing of you and earns
      attention anyway, which is what makes it so easy to overlook and so
      hard to do well.
    </p>
    <blockquote>
      The reader will not thank you for shouting, but a whisper too soft
      to hear is worse than a shout you can ignore.
    </blockquote>
    <p>
      Every preset on this page is asked to render the same paragraph;
      what changes is the voice it speaks in.
    </p>
  </article>

  <!-- Tag / chip cluster -->
  <div class="cluster">
    <span class="tag success">Success</span>
    <span class="tag warning">Warning</span>
    <span class="tag info">Info</span>
    <span class="tag">Neutral</span>
  </div>
</section>

<style>
  .canonical-fixture {
    container-type: inline-size;
  }
  /* Inline the open dialog inside the fixture so each preset's dialog
     surface renders in flow rather than the browser-default top-layer
     position. Visual demo only — real consumers use showModal(). */
  .canonical-fixture :global(dialog[open]) {
    position: static;
    margin: 0;
    inset: auto;
    max-width: 100%;
    background: var(--bg);
    color: var(--fg);
    border: 1px solid var(--fg-2);
    border-radius: var(--br-m);
    box-shadow: var(--shadow-3);
    padding: var(--pad-l);
  }
</style>
