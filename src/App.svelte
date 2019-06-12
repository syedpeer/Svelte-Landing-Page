<script>
  import MainText from "./MainText.svelte";
  import Settings from "./Settings.svelte";

  const images = {
    "Landscape 1": { href: "./img/landscape1.jpg", textColor: "#333" },
    "Landscape 2": { href: "./img/landscape2.jpg", textColor: "white" },
    "Landscape 3": { href: "./img/landscape3.jpg", textColor: "white" }
  };

  let currentImage = "Landscape 1";
  $: currentImageUrl = images[currentImage].href;
  $: currentTextColor = images[currentImage].textColor;

  let settingsPage = false;

  const toggleSettingsView = () => {
    settingsPage = !settingsPage;
  };

  const updateImage = image => {
    currentImage = image.detail;
  };
</script>

<style>
  main {
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    height: 100vh;
    background-size: cover;
  }

  img {
    position: absolute;
    right: 1rem;
    bottom: 1rem;
    height: 60px;
    cursor: pointer;
  }
</style>

<main style="background-image: url({currentImageUrl})">
  <MainText color={currentTextColor} />
  <img
    src="/icons/settings.png"
    alt="Settings icon"
    on:click={toggleSettingsView} />
  {#if settingsPage}
    <Settings
      on:close={toggleSettingsView}
      on:updateimage={updateImage}
      {images}
      {currentImage} />
  {/if}
</main>
