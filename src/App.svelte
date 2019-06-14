<script>
  import MainText from "./MainText.svelte";
  import Settings from "./Settings.svelte";
  import Tools from "./Tools.svelte";

  const images = {
    "Landscape 1": { href: "./img/landscape1.jpg", textColor: "#333" },
    "Landscape 2": { href: "./img/landscape2.jpg", textColor: "white" },
    "Landscape 3": { href: "./img/landscape3.jpg", textColor: "white" }
  };

  let currentImage = "Landscape 1";
  $: currentImageUrl = images[currentImage].href;
  $: currentTextColor = images[currentImage].textColor;

  const pages = ["main", "tools"];
  let currentPageIndex = 0;
  $: currentPage = pages[currentPageIndex];

  let settingsPage = false;

  const toggleSettingsView = () => {
    settingsPage = !settingsPage;
  };

  const updateImage = image => {
    currentImage = image.detail;
  };

  const toRightPage = () => {
    currentPageIndex++;
  };

  const toLeftPage = () => {
    currentPageIndex--;
  };
</script>

<style>
  main {
    display: flex;
    justify-content: space-between;
    align-items: center;
    text-align: center;
    height: 100vh;
    background-size: cover;
  }

  div.nav-arrow {
    height: 100vh;
    display: flex;
    align-items: center;
    cursor: pointer;
  }

  div.nav-arrow-left {
    margin-left: 1rem;
  }

  div.nav-arrow-right {
    margin-right: 1rem;
  }

  i {
    font-size: 5em;
    font-stretch: ultra-expanded;
    color: rgb(150, 144, 144);
  }

  img {
    position: absolute;
    right: 1rem;
    bottom: 1rem;
    height: 60px;
    cursor: pointer;
  }
</style>

<svelte:head>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css" />
</svelte:head>

<main style="background-image: url({currentImageUrl})">
  <div class="nav-arrow nav-arrow-left" on:click={toLeftPage}>
    <i class="fa fa-chevron-left" />
  </div>
  {#if currentPage === 'main'}
    <MainText color={currentTextColor} />
  {:else if currentPage === 'tools'}
    <Tools />
  {/if}
  <div class="nav-arrow nav-arrow-right" on:click={toRightPage}>
    <i class="fa fa-chevron-right" />
  </div>
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
