<script lang="ts">
  import SvelteIntersectionObserver from "../types";
  import type { Entry } from "../types/IntersectionObserver.svelte";
  import IO from "../types/IntersectionObserver.svelte";

  let intersecting = false;
  let entry: Entry = null;
  let element: HTMLElement;
  let observer: IntersectionObserver;

  $: inView = entry && entry.isIntersecting;
</script>

<header>
  <strong>Scroll down.</strong>
  <div>
    Element in view?
    <strong class="answer" class:inView>{inView ? "Yes" : "No"}</strong>
  </div>
</header>

<!-- svelte-ignore missing-declaration -->
<SvelteIntersectionObserver {element} bind:entry bind:intersecting>
  <div class="element" bind:this={element}>
    {#if inView}Element is in view{/if}
  </div>
</SvelteIntersectionObserver>

<!-- svelte-ignore missing-declaration -->
<SvelteIntersectionObserver
  {element}
  bind:observer
  on:intersect={(e) => {
    console.log(e.detail);
  }}
>
  <div bind:this={element}>Hello world</div>
</SvelteIntersectionObserver>

<!-- svelte-ignore missing-declaration -->
<IO
  on:observe={(e) => {
    console.log(e.detail);
    console.log(e.detail.intersectionRect);
    console.log(e.detail.isIntersecting); // boolean
  }}
  on:intersect={(e) => {
    console.log(e.detail.isIntersecting); // true
  }}
/>
