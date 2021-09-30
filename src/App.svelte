<script lang="ts">
  import Slide from "./components/Slide.svelte";
  console.log("I'm app!");

  let testMarkdown: string = `
  # Svelte

Cybernetically enhanced web apps! 
^
|
|
WTF?

* This is a list
* With two items
  1. And a sublist
  2. That is ordered
    * With another
    * Sublist inside

| And this is | A table |
|-------------|---------|
| With two    | columns |`;
</script>

<main>
  <!-- <h1>derp</h1>
  <p>herp</p> -->
  <Slide markdown={testMarkdown} />
</main>

<style>
  :global(:root) {
    --pal-primary: #fe7f2d;
    --pal-secondary: #619b8a;
    --pal-highlight: #fcca46;
    --pal-bg-dark: #233d4d;
    --pal-bg-light: #a1c181;
  }

  main {
    height: 100%;
    width: 100%;
    background-color: var(--pal-bg-dark);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  :global(h1, h2, h3, h4, h5, h6) {
    font-family: "Raleway", sans-serif;
    color: var(--pal-primary);
  }
  :global(p) {
    font-family: "Raleway", sans-serif;
    color: var(--pal-secondary);
  }
</style>
