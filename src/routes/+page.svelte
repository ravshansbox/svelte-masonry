<script>
  import MasonryLayout from 'src/components/MasonryLayout.svelte';

  const items = new Array(50).fill(null).map((_element, index) => ({
    id: index,
    height: Math.round(Math.random() * 100 + 50),
  }));

  const onLayoutComplete = () => {
    console.log('layout complete');
  };
</script>

<MasonryLayout
  {items}
  let:item
  className="container"
  on:layoutComplete={onLayoutComplete}
>
  <div class="item" style:height="{item.height}px">
    {item.id}
  </div>
</MasonryLayout>

<style>
  :global(.container) {
    display: flex;
    gap: 4px;
  }
  .item {
    align-items: center;
    border: 1px solid grey;
    display: flex;
    justify-content: center;
    width: 25%;
  }
</style>
