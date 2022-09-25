<script lang="ts">
  import chroma from 'chroma-js';
  import { kebabize } from '../utils';
  import type { RangeHue } from '../utils';
  export let text = 'Minecraft';
  export let size = 1;
  export let hue: RangeHue = 194;
  export let animate = true;
  export let colorTheme: 'light' | 'dark' = 'dark';

  let colorScheme: { [key: string]: string }, colorSchemeCSS: string;

  $: {
    if (colorTheme === 'dark') {
      colorScheme = {
        colorAccentBase: chroma.hsl(hue, 1, 0.65).hex('rgb'),
        colorAccentBaseHover: chroma.hsl(hue - 1, 1, 0.72).hex('rgb'),
        colorAccentTop: chroma.hsl(hue - 5, 1, 0.84).hex('rgb'),
        colorAccentLeft: chroma.hsl(hue + 3, 0.81, 0.58).hex('rgb'),
        colorAccentRight: chroma.hsl(hue + 3, 0.81, 0.58).hex('rgb'),
        colorAccentBottom: chroma.hsl(hue + 3, 0.81, 0.58).hex('rgb'),
        colorAccentShadow: chroma.hsl(hue + 3, 0.81, 0.58).hex('rgb'),
        colorAccentText: chroma.hsl(hue + 26, 0.1, 0.11).hex('rgb'),
      };
    } else if (colorTheme === 'light') {
      colorScheme = {
        colorAccentBase: chroma.hsl(hue, 0.88, 0.31).hex('rgb'),
        colorAccentBaseHover: chroma.hsl(hue - 1, 1, 0.27).hex('rgb'),
        colorAccentTop: chroma.hsl(hue - 5, 0.68, 0.48).hex('rgb'),
        colorAccentLeft: chroma.hsl(hue + 3, 0.8, 0.24).hex('rgb'),
        colorAccentRight: chroma.hsl(hue + 3, 0.8, 0.24).hex('rgb'),
        colorAccentBottom: chroma.hsl(hue + 3, 0.86, 0.16).hex('rgb'),
        colorAccentShadow: chroma.hsl(hue + 3, 1, 0.15).hex('rgb'),
        colorAccentText: chroma.hsl(0, 0, 1).hex('rgb'),
      };
    }
  }

  $: colorSchemeCSS =
    Object.entries(colorScheme)
      .map(([key, value]) => {
        return `--${kebabize(key)}: ${value}`;
      })
      .join('; ') + (animate ? '' : '; --animation-timing: 0s');
</script>

<button style="--font-size: {size}rem; {colorSchemeCSS}">
  <div class="border top" />
  <div class="border bottom" />
  <div class="border left" />
  <div class="border right" />
  <div class="border border-black-h" />
  <div class="border border-black-w" />
  <div class="content">
    <p class="text">
      {text}
    </p>
  </div>
</button>

<style>
  :root {
    --color-accent-base: hsl(194, 100%, 65%);
    --color-accent-base-hover: hsl(193, 100%, 72%);
    --color-accent-top: hsl(189, 100%, 84%);
    --color-accent-left: hsl(197, 81%, 58%);
    --color-accent-right: hsl(197, 81%, 58%);
    --color-accent-bottom: hsl(197, 81%, 58%);
    --color-accent-shadow: hsl(197, 81%, 58%);
    --color-accent-text: hsl(220, 100%, 11%);

    --coldor-accent-base-light: hsl(150, 88%, 31%);
    --coldor-accent-base-hover-light: hsl(150, 100%, 27%);
    --coldor-accent-top-light: hsl(129, 68%, 48%);
    --coldor-accent-left-light: hsl(150, 80%, 24%);
    --coldor-accent-right-light: hsl(150, 80%, 24%);
    --coldor-accent-bottom-light: hsl(150, 86%, 16%);
    --coldor-accent-shadow-light: hsl(157, 100%, 15%);
    --coldor-accent-text-light: hsl(0, 0%, 100%);

    --shadow-color: rgba(255, 255, 255, 1);

    --shadow-offset-max: 1em;

    --font-size: 0.8rem;

    --animation-curve: cubic-bezier(0.75, 0.35, 0.25, 0.88);
    --animation-timing: 1s;
    --border-thickness: 0.2em;
    --border-border-thickness: 0.1em;
    --border-color: black;
    --border-color-active: white;

    --thickness: calc(var(--border-thickness) + var(--border-border-thickness));
  }

  button {
    margin: 0;
    padding: 0;
    border-radius: 0;
    border: none;
    position: relative;
    font-size: var(--font-size);
    transition: transform 0.2s ease;
    margin: var(--thickness);
    outline: none;
  }

  .content {
    padding: 0.4rem 0.4rem;
    background-color: var(--color-accent-base);
    /* z-index: 2; */
  }

  button:hover .content {
    background-color: var(--color-accent-base-hover);
  }

  button:active {
    transform: translateY(5%);
  }

  button::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    animation: shadow var(--animation-timing) alternate infinite
      var(--animation-curve);
    will-change: filter;
    z-index: -4;
    background-color: black;
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
    font-family: 'Minecraft', sans-serif;
    animation: zimzoom var(--animation-timing) alternate infinite
      var(--animation-curve);
    text-shadow: 0 0.1em var(--color-accent-shadow);
    color: var(--color-accent-text);
    z-index: 2;
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
    background-color: var(--border-color);
  }

  .border-black-w {
    top: calc(-1 * (var(--border-border-thickness)));
    left: calc(var(--thickness) * -1);
    position: absolute;
    height: calc(100% + var(--border-border-thickness) * 2);
    width: calc(100% + var(--thickness) * 2);
    background-color: var(--border-color);
  }

  button:is(:active, :focus) :is(.border-black-h, .border-black-w) {
    background-color: var(--border-color-active);
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
    height: calc(0.2em + var(--border-thickness));
    background-color: var(--color-accent-top);
  }
  .bottom {
    bottom: calc(var(--border-thickness) * -1);
    left: 0;
    width: 100%;
    height: calc(0.2em + var(--border-thickness));
    background-color: var(--color-accent-bottom);
  }
  .left {
    top: 0;
    left: calc(var(--border-thickness) * -1);
    width: calc(0.2em + var(--border-thickness));
    height: 100%;
    background-color: var(--color-accent-left);
  }
  .right {
    top: 0;
    right: calc(var(--border-thickness) * -1);
    width: calc(0.2em + var(--border-thickness));
    height: 100%;
    background-color: var(--color-accent-right);
  }

  @keyframes zimzoom {
    from {
      transform: scale(1);
    }

    to {
      transform: scale(1.1);
    }
  }
</style>
