<script lang="ts">
  import MinecraftButton from './lib/MinecraftButton.svelte';
  let text = 'New trailer';
  let size = 3;
</script>

<svelte:head>
  <title>😢 Issue with the "new trailer" minecraft launcher button</title>
</svelte:head>

<header>
  <h1>😢 Issue with the "new trailer" Minecraft launcher button</h1>
</header>
<main>
  <p>
    When I recently launched the Minecraft launcher, I was obviously curious
    about the <em>brand new game</em> from
    <a
      href="https://upload.wikimedia.org/wikipedia/fr/0/01/Mojang_Studios_Logo_SVG.svg"
    >
      <img
        class="mojang"
        src="https://upload.wikimedia.org/wikipedia/fr/0/01/Mojang_Studios_Logo_SVG.svg"
        alt="Mojang"
      />
    </a>
    displayed on the sidebar :
  </p>
  <a
    href="https://static.wikia.nocookie.net/logopedia/images/7/7d/Minecraft_Legends_logo.png"
  >
    <img
      height="100px"
      src="/Minecraft_Legends_logo.png"
      alt="Logo minecraft legends"
      style="height: 100px;"
    />
  </a>

  <p>
    Unfortunately, I also noticed a problem with their button/link to the game's
    trailer (my pc is french) :
  </p>
  <video src="/fail.mp4" autoplay loop>
    <track kind="captions" />
  </video>
  <p>
    So I chose to reimplement the button using pure
    <span class="cybernetic"> SVELTE (Cybernetically enhanced web apps)</span>
    and CSS and 🎉TADA🎉 :
  </p>

  <form>
    <div>
      <label for="text"><b>Choose the text within the button</b></label>
      <input id="text" name="text" type="text" bind:value={text} />
    </div>
    <div>
      <label for="size"><b>Change the size of the element</b></label>
      <input
        type="range"
        name="size"
        id="size"
        min="0.25"
        step=".25"
        max="10"
        bind:value={size}
      />
    </div>
  </form>
  <div class="button">
    <MinecraftButton {text} {size} />
  </div>
</main>

<footer>
  Me, the author, <a href="https://sacha.house">Sacha FROMENT</a> at your service
  😎
</footer>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Overpass&display=swap');
  form {
    margin: 1rem auto;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }

  .mojang {
    display: inline-block;
    margin: 0 0.2rem;
    height: 0.8rem;
    justify-self: center;
  }

  .cybernetic {
    font-family: 'Overpass', -apple-system, BlinkMacSystemFont, 'Segoe UI',
      Roboto, Oxygen, Ubuntu, Cantarell, 'Fira Sans', 'Droid Sans',
      'Helvetica Neue', sans-serif;
  }

  .button {
    margin: 2rem auto;
    display: flex;
    place-content: center;
    /* background-color: rgba(175, 175, 175, 0.5); */
    padding: 0.5rem;
    border-radius: 0.5rem;
    /* border: 1px solid rgba(70, 70, 70, 0.2); */
  }

  h1 {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  }
  input {
    min-width: fit-content;
    padding: 0.5rem;
  }
  video {
    margin: 1rem auto;
    display: block;
  }
</style>
