<script>
  import { onMount } from 'svelte';
  export let id;
  export let onEnter;
  let el;

  onMount(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          onEnter(id);
        }
      },
      { threshold: 0.5 }
    );
    observer.observe(el);
    return () => observer.disconnect();
  });
</script>

<div bind:this={el} class="scroll-section">
  <slot />
</div>

<style>
.scroll-section {
  margin: 6rem 0;
  min-height: 60vh;
}
</style>
