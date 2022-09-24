<script lang="ts">
  export let text = 'Minecraft';
  export let size = 1;
</script>

<button style="--font-size: {size}rem">
  <div class="border top" />
  <div class="border bottom" />
  <div class="border left" />
  <div class="border right" />
  <div class="border border-black-h" />
  <div class="border border-black-w" />
  <p class="text">
    {text}
  </p>
</button>

<style>
  @import url('https://fonts.cdnfonts.com/css/minecraft-4');

  :root {
    --blue-shadow: #3fb9eb;
    --blue-left: #3fb9eb;
    --blue-right: #3fb9eb;
    --blue-top: #acf2ff;
    --blue-bottom: #3fb9eb;
    --blue-main: #4ad5ff;
    --blue-main-hover: #70dfff;
    --text-color: #001236;

    --shadow-color: rgba(255, 255, 255, 1);

    --shadow-offset-max: 2em;

    --font-size: 1rem;

    --animate-rythm: cubic-bezier(0.75, 0.35, 0.25, 0.88);
    --border-thickness: 0.2em;
    --border-border-thickness: 0.1em;

    --thickness: calc(var(--border-thickness) + var(--border-border-thickness));
  }

  button {
    padding: 0.4rem 0.4rem;
    margin: var(--thickness);
    border-radius: 0;
    border: none;
    position: relative;
    cursor: pointer;
    font-size: var(--font-size);
    background-color: var(--blue-main);
  }

  button:hover {
    background-color: var(--blue-main-hover);
  }

  button::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    animation: shadow 1s alternate infinite var(--animate-rythm);
    will-change: filter;
    z-index: -4;
    background-color: white;
  }

  @keyframes shadow {
    from {
      filter: none;
    }
    to {
      filter: drop-shadow(0 0 var(--shadow-offset-max) var(--shadow-color));
    }
  }

  .text {
    margin: 0.3em 1.4em;
    margin-bottom: 0.4em;
    padding-bottom: em;
    font-family: 'Minecraft', sans-serif;
    animation: zimzoom 1s alternate infinite var(--animate-rythm);
    text-shadow: 0 0.1em var(--blue-shadow);
    color: var(--text-color);
  }

  .border {
    position: absolute;
    z-index: -2;
  }

  .border-black-h {
    top: calc(var(--thickness) * -1);
    left: calc(-1 * (var(--border-border-thickness)));
    position: absolute;
    height: calc(100% + var(--thickness) * 2);
    width: calc(100% + var(--border-border-thickness) * 2);
    background-color: black;
  }

  .border-black-w {
    top: calc(-1 * (var(--border-border-thickness)));
    left: calc(var(--thickness) * -1);
    position: absolute;
    height: calc(100% + var(--border-border-thickness) * 2);
    width: calc(100% + var(--thickness) * 2);
    background-color: black;
  }

  .top,
  .bottom,
  .left,
  .right {
    z-index: -1;
  }

  .top,
  .bottom {
    height: var(--border-thickness);
    width: 100%;
  }
  .left,
  .right {
    height: 100%;
    width: var(--border-thickness);
  }

  .top {
    top: calc(var(--border-thickness) * -1);
    left: 0;
    width: 100%;
    height: calc(1em + var(--border-thickness));
    background-color: var(--blue-top);
  }
  .bottom {
    bottom: calc(var(--border-thickness) * -1);
    left: 0;
    width: 100%;
    height: calc(1em + var(--border-thickness));
    background-color: var(--blue-bottom);
  }
  .left {
    top: 0;
    left: calc(var(--border-thickness) * -1);
    width: calc(1em + var(--border-thickness));
    height: 100%;
    background-color: var(--blue-left);
  }
  .right {
    top: 0;
    right: calc(var(--border-thickness) * -1);
    width: calc(1em + var(--border-thickness));
    height: 100%;
    background-color: var(--blue-right);
  }

  @keyframes zimzoom {
    from {
      transform: scale(1);
    }

    to {
      transform: scale(1.2) translateY(-0.2rem);
    }
  }
</style>
