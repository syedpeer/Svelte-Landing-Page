<script>
  const tools = {
    colorPicker: {
      text: "Color Picker",
      backgroundImage: "https://www.w3schools.com/colors/img_colormap.gif",
      backgroundColor: "rgba(51, 204, 51, 0.5)"
    },
    smartschool: {
      text: "Smartschool",
      backgroundImage:
        "https://hhh.smartschool.be/smsc/svg/logo_smartschool/logo_smartschool_16x16.svg",
      backgroundColor: "orange"
    },
    github: {
      text: "Github",
      backgroundImage: "https://image.flaticon.com/icons/svg/25/25231.svg",
      backgroundColor: "grey"
    },
    codesandbox: {
      text: "CodeSandbox.io",
      backgroundImage: "/tool-tiles-backgroundimgs/codesandbox-icon.svg",
      backgroundColor: "rgba(0, 0, 0, 0.5)"
    },
    codecademy: {
      text: "CodeCademy",
      backgroundImage:
        "https://www.codecademy.com/webpack/1cd00f03e7d4e31bf2c59d363fd154ff.svg",
      backgroundColor: "rgba(153, 51, 153, 0.9)"
    },
    irccloud: {
      text: "IRCCloud",
      backgroundImage:
        "http://lh3.ggpht.com/6dbDUfjcsEqWaUxfjkNMY5Obo_1xS6LcxTt3DBetr9MfkkYd6swzdsDmWmo41PTkU54O",
      backgroundColor: "rgba(0, 0, 255, 0.5)"
    }
  };

  const toolNames = Object.keys(tools);
</script>

<style>
  div.tool-tiles {
    display: grid;
    width: 55vw;
    height: 60vh;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 2rem;
  }

  div.tool-tile {
    max-height: 70%;
    background-blend-mode: multiply;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2.5rem;
    font-weight: 700;
    cursor: pointer;
    background-repeat: no-repeat;
    background-size: cover;
  }
</style>

<div class="tool-tiles">
  {#each toolNames as tool}
    <div
      class="tool-tile"
      style="background-image: url({tools[tool].backgroundImage});
      background-color: {tools[tool].backgroundColor};">
      <span
        style="color: {tools[tool].textColor ? tools[tool].textColor : 'white'}">
         {tools[tool].text}
      </span>
    </div>
  {/each}
</div>
