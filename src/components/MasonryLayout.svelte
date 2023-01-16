<script lang="ts">
  import MasonryLayout from 'masonry-layout';
  import { createEventDispatcher, onDestroy, onMount } from 'svelte';

  type T = $$Generic<{ id: string | number }>;

  export let items: T[];
  export let className: string | null = null;
  export let percentPosition = true;
  export let transitionDuration: string | 0 = 0;

  let element: HTMLElement;
  let masonry: MasonryLayout;

  const dispatch = createEventDispatcher<{
    layoutComplete: T[];
  }>();

  onMount(() => {
    if (element) {
      masonry = new MasonryLayout(element, {
        percentPosition,
        transitionDuration,
      });
      masonry.on?.('layoutComplete', (items: T[]) => {
        dispatch('layoutComplete', items);
      });
    }
  });

  onDestroy(() => {
    masonry?.destroy?.();
  });
</script>

<div bind:this={element} class={className}>
  {#each items as item, index (item.id)}
    <slot {item} {index} />
  {/each}
</div>
