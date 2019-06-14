<script>
  export let max;
  export let current;

  const dots = [];
  for (let i = 0; i < max; i++) {
    dots.push(i);
  }
</script>

<style>
  div.page-indicator-container {
    position: absolute;
    bottom: 1.5rem;
    left: 45%;
    right: 45%;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 10vw;
    height: 1.5rem;
    margin: auto;
  }

  div.page-indicator-dot {
    border-radius: 50%;
    height: 1rem;
    width: 1rem;
    border: 3px solid white;
    background-color: white;
  }

  div.page-indicator-dot + div.page-indicator-dot {
    margin: 0 5px;
  }

  div.page-indicator-dot.current {
    background-color: #333;
  }
</style>

<div class="page-indicator-container">
  {#each dots as dot}
    <div class="page-indicator-dot {current === dot ? 'current' : ''}" />
  {/each}
</div>
