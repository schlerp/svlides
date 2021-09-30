<script lang="ts">
  import { fade } from "svelte/transition";
  import SvelteMarkdown from "svelte-markdown";

  export let markdown: string;
</script>

<div class="slide" in:fade={{ duration: 2000 }} out:fade={{ duration: 2000 }}>
  <SvelteMarkdown source={markdown} />
</div>

<style>
  .slide {
    height: 100%;
    width: 100%;
    background-color: inherit;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: inherit;
    transition: all 2000ms;
  }
</style>
