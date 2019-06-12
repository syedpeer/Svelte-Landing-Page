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
</script>

<style>
  h1.timer {
    font-size: 6em;
  }
</style>

<div class="main-text" style="color: {color}">
  <h1 class="greeting">Good {timeOfDay}, Josse!</h1>
  <h1 class="timer">{`${hour}:${minutes}:${seconds}`}</h1>
</div>
