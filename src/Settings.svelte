<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  export let images;
  export let currentImage;
  const imageNames = Object.keys(images);

  const close = () => {
    dispatch("close");
  };
</script>

<style>
  .settings {
    position: absolute;
    top: 5rem;
    bottom: 5rem;
    left: 3rem;
    right: 3rem;
    text-align: center;
    background-color: white;
    border-radius: 2rem;
    padding: 1.5rem;
    box-shadow: 0 0 2rem rgba(0, 0, 0, 0.5);
  }

  h1,
  h2 {
    padding-bottom: 3px;
    margin-bottom: 1em;
  }

  h1.header {
    border-bottom: 1px solid rgba(128, 128, 128, 0.644);
  }

  span.close-icon {
    position: absolute;
    top: 1rem;
    right: 2rem;
    font-size: 2em;
    font-weight: 700;
    cursor: pointer;
  }

  h2.subheader {
    text-align: left;
  }

  div.image-tiles-container {
    display: flex;
  }

  div.image-tile {
    height: 200px;
    width: 355px;
    background-size: cover;
    background-color: grey;
    background-blend-mode: multiply;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
  }

  div.image-tile + div.image-tile {
    margin-left: 4em;
  }

  div.image-tile.current {
    border: 8px solid darkgreen;
  }

  div.image-tile p {
    color: white;
    font-size: 1.5em;
  }

  button.close-btn {
    display: block;
    background-color: green;
    color: white;
    cursor: pointer;
    padding: 0.5em 1em;
    margin: 1em auto;
    border: 1px solid rgb(11, 73, 11);
    border-radius: 5px;
  }

  button.close-btn:hover {
    background-color: rgb(7, 94, 7);
  }
</style>

<div class="settings">
  <h1 class="header">Settings</h1>
  <span class="close-icon" on:click={close}>x</span>
  <h2 class="subheader">Background</h2>
  <div class="image-tiles-container">
    {#each imageNames as image}
      <div
        class="image-tile{image === currentImage ? ' current' : ''}"
        style="background-image: url({images[image].href})"
        on:click={() => dispatch('updateimage', image)}>
        <p>{image}</p>
      </div>
    {/each}
  </div>
  <button class="close-btn" on:click={close}>Save and close</button>
</div>
