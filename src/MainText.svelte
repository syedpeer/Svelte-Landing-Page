<script>
  export let color;
  let date = new Date();
  let timeOfDay;

  $: hour = date.getHours();
  $: rawMinutes = date.getMinutes();
  $: rawSeconds = date.getSeconds();

  $: minutes = rawMinutes >= 10 ? rawMinutes : "0" + rawMinutes;
  $: seconds = rawSeconds >= 10 ? rawSeconds : "0" + rawSeconds;

  const getTimeOfDay = async () => {
    await hour;
    if (hour > 7 && hour < 12) {
      timeOfDay = "morning";
    } else if (hour >= 12 && hour < 17) {
      timeOfDay = "afternoon";
    } else if (hour >= 17 && hour < 21) {
      timeOfDay = "evening";
    } else {
      timeOfDay = "night";
    }
  };

  $: getTimeOfDay();

  setInterval(() => {
    date = new Date();
  }, 1000);

  let searchTerms = "";

  const search = () => {
    const encodedSearchTerms = searchTerms.replace(" ", "%20");
    window.open(`https://ecosia.org/search?q=${encodedSearchTerms}`);
    searchTerms = "";
  };
</script>

<style>
  h1.timer {
    font-size: 6em;
  }

  .searchbar-container {
    margin-top: 2rem;
    width: 45em;
    border: none;
    border-radius: 1rem;
    overflow: hidden;
    background-color: white;
  }

  .searchbar {
    width: 80%;
    padding: 1em;
    border: none;
  }

  .search-button {
    width: 18%;
    height: 2.2rem;
    background-color: rgb(7, 7, 168);
    color: white;
    border: none;
    border-radius: 1rem;
    cursor: pointer;
  }
</style>

<div class="main-text" style="color: {color}">
  <h1 class="greeting">Good {timeOfDay}, Josse!</h1>
  <h1 class="timer">{`${hour}:${minutes}:${seconds}`}</h1>
  <div class="searchbar-container">
    <input
      type="text"
      bind:value={searchTerms}
      class="searchbar"
      placeholder="Search on Ecosia..."
      on:keypress={event => {
        if (event.key === 'Enter') search();
      }} />
    <button class="search-button" on:click={search}>
      <i class="fa fa-search" />
    </button>
  </div>
</div>
