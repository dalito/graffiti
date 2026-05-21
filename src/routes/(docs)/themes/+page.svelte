<script>
  import CanonicalFixture from "$docs/CanonicalFixture.svelte";

  // Pulls all 5 preset CSS files into the page (does NOT apply any theme-* class
  // to <html>, so the per-section wrapping below carries the theme scope).
  import "$lib/themes/editorial.css";
  import "$lib/themes/paper.css";
  import "$lib/themes/brutalist.css";
  import "$lib/themes/neon-arcade.css";
  import "$lib/themes/soft-consumer.css";

  const presets = [
    { name: "editorial", label: "theme-editorial" },
    { name: "paper", label: "theme-paper" },
    { name: "brutalist", label: "theme-brutalist" },
    { name: "neon-arcade", label: "theme-neon-arcade" },
    { name: "soft-consumer", label: "theme-soft-consumer" },
  ];
</script>

<svelte:head>
  <title>Themes — Graffiti</title>
  <link
    rel="preconnect"
    href="https://fonts.googleapis.com"
  />
  <link
    rel="preconnect"
    href="https://fonts.gstatic.com"
    crossorigin
  />
  <link
    href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght,SOFT,WONK@0,9..144,100..900,0..100,0..1;1,9..144,100..900,0..100,0..1&family=Big+Shoulders+Display:wght@100..900&family=Space+Grotesk:wght@300..700&family=Inter:wght@100..900&family=DM+Sans:ital,opsz,wght@0,9..40,100..1000;1,9..40,100..1000&display=swap"
    rel="stylesheet"
  />
</svelte:head>

<section class="stack readable">
  <h1>Aesthetic presets</h1>
  <p class="pull-quote">
    Five token-dominant presets, each wrapped on a container so they re-skin
    only their subtree. Same markup, different voice. Inspect to see how each
    preset reaches the same six surface types: buttons, cards, forms,
    dialogs, prose, and tags.
  </p>
</section>

{#each presets as preset (preset.name)}
  <section class={`theme-${preset.name} theme-fixture-section`}>
    <h2 class="theme-fixture-label">.{preset.label}</h2>
    <CanonicalFixture />
  </section>
{/each}

<style>
  .theme-fixture-section {
    background: var(--bg);
    color: var(--fg);
    padding-block: var(--vs-xl);
    padding-inline: var(--pad-l);
    margin-block: var(--vs-l);
    border-radius: var(--br-m);
  }

  .theme-fixture-label {
    font-family: var(--font-mono, ui-monospace, monospace);
    font-size: 0.9em;
    opacity: 0.7;
    margin-block-end: var(--vs-base);
    text-transform: none;
    letter-spacing: 0;
  }
</style>
