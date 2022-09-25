<script lang="ts">
  import Clipboard from 'svelte-clipboard';
  import { onMount } from 'svelte';
  import MinecraftButton from './lib/MinecraftButton.svelte';
  import type { RangeHue } from './utils';

  const TEXT_PARAM = 'text';
  const SIZE_PARAM = 'size';
  const HUE_PARAM = 'hue';
  const ANIMATE_PARAM = 'animate';
  const DARK_PARAM = 'dark';

  let text = 'NEW TRAILER';
  let size = 2;
  let hue: RangeHue = 194;
  let animate = true;
  let darkToggle = true;
  let colorTheme: 'light' | 'dark' = 'dark';
  let loaded = false;
  $: colorTheme = darkToggle ? 'dark' : 'light';
  $: {
    if (loaded) {
      const params = new URLSearchParams(window.location.search);
      params.set(TEXT_PARAM, text);
      params.set(SIZE_PARAM, size.toString());
      params.set(HUE_PARAM, hue.toString());
      params.set(ANIMATE_PARAM, animate.toString());
      params.set(DARK_PARAM, darkToggle.toString());
      const { pathname } = location;
      const stateObj = {
        title: `Recherche : ${text}`,
        url: text ? `${pathname}?${params}` : pathname,
      };
      history.pushState(stateObj, stateObj.title, stateObj.url);
    }
  }
  onMount(() => {
    const params = new URLSearchParams(location.search);
    const textParam = params.get(TEXT_PARAM);
    const sizeParam = params.get(SIZE_PARAM);
    const hueParam = params.get(HUE_PARAM);
    const animateParam = params.get(ANIMATE_PARAM);
    const darkParam = params.get(DARK_PARAM);
    if (textParam) {
      text = textParam;
    }
    if (sizeParam) {
      size = parseFloat(sizeParam);
    }
    if (hueParam) {
      hue = (parseInt(hueParam) % 360) as RangeHue;
    }
    if (animateParam === 'true' || animateParam === 'false') {
      animate = JSON.parse(animateParam) as boolean;
    }
    if (darkParam === 'true' || darkParam === 'false') {
      darkToggle = JSON.parse(darkParam) as boolean;
    }
    loaded = true;
  });
</script>

<svelte:head>
  <title>Issue with the "new trailer" minecraft launcher button</title>
</svelte:head>

<article>
  <header>
    <h1>⛏️ Issue with the "new trailer" Minecraft launcher <u>button</u></h1>
  </header>
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
      class="legends"
      src="/Minecraft_Legends_logo.png"
      alt="Logo minecraft legends"
    />
  </a>

  <p>
    Unfortunately, I also noticed a problem with their <u>button/link</u> to the
    game's trailer (my pc is french) :
  </p>
  <video src="/fail.mp4" autoplay loop controls>
    <track kind="captions" />
  </video>
  <p>
    So I chose to reimplement the button using <u
      >pure
      <span class="cybernetic"> SVELTE (Cybernetically enhanced web apps)</span>
      and CSS</u
    > and 🎉TADA🎉 :
  </p>

  <section class="demo">
    <p>You can modify :</p>
    <div class="actions">
      <div class="action">
        <label for="hue"><b>The hue... </b></label>
        <input
          type="range"
          name="hue"
          min={0}
          max={359}
          id="hue"
          bind:value={hue}
        />
      </div>
      <div class="action">
        <label for="text"><b>...the text... </b></label>
        <input id="text" name="text" type="text" bind:value={text} />
      </div>
      <div class="action">
        <label for="dark"
          ><b
            >...the color theme/variant (current = <em>{colorTheme}</em>) ...
          </b></label
        >
        <input
          id="dark"
          name="dark"
          type="checkbox"
          bind:checked={darkToggle}
        />
      </div>
      <div class="action">
        <label for="animate"><b>...wether or not to animate... </b></label>
        <input
          id="animate"
          name="animate"
          type="checkbox"
          bind:checked={animate}
        />
      </div>
      <div class="action">
        <label for="size"><b>...or the size</b></label>
        <input
          type="range"
          name="size"
          id="size"
          min="0.25"
          step=".05"
          max="5"
          bind:value={size}
        />
      </div>
    </div>
    <Clipboard
      text={(() => {
        return location.toString();
      })()}
      let:copy
      on:copy={() => {
        alert(
          `You now have your custom button URL in your clipboard ! 🎉`
        );
      }}
    >
      <button on:click={copy} class="share"
        >📋 Copy your <b>custom button URL</b> to the clipboard !</button
      >
    </Clipboard>

    <div class="button">
      <MinecraftButton {text} {size} {hue} {animate} {colorTheme} />
    </div>
  </section>
</article>

<footer>
  <p>
    Me, the author, <a href="https://sacha.house">Sacha FROMENT</a> at your service
    😎.
  </p>
  <p>
    <a href="https://gitlab.com/sachahjkl/button.sacha.house"
      >⌨️ Source code for this page</a
    >
  </p>
</footer>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Overpass&display=swap');

  .actions {
    margin: 1rem auto;
    /* display: flex; */
    justify-content: space-around;
  }

  .action {
    margin: 1rem auto;
  }
  .action > input:not([type='checkbox']) {
    flex: 1 1 100%;
  }

  .share {
    padding: 0.25rem 0.5rem;
  }

  footer {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
    border-top: var(--text-color);
  }

  .legends {
    max-height: 100px;
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
    margin: 6rem auto;
    display: flex;
    place-content: center;
    /* background-color: rgba(175, 175, 175, 0.5); */
    padding: 0.5rem;
    border-radius: 0.5rem;
    /* border: 1px solid rgba(70, 70, 70, 0.2); */
  }

  h1 {
    font-size: 2rem;
  }
  video {
    display: block;
    max-width: 80%;
  }
  label {
    margin-bottom: 4px;
    display: block;
  }
  input {
    display: block;
    width: 80%;
    margin: 0.5rem;
  }
  input[type='checkbox'] {
    width: auto;
  }
  input[type='text'] {
    padding: 0.5rem;
  }
  img,
  video {
    margin: 2rem auto;
  }
</style>
