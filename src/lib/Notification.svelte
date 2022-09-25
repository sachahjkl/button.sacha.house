<script lang="ts">
  import { fly } from 'svelte/transition';
  import { circIn } from 'svelte/easing';
  import { createEventDispatcher } from 'svelte';
  export let show = false;
  export let title = 'Notification title';
  export let message = 'Notification message !';
  const dispatch = createEventDispatcher();
  function click() {
    dispatch('click');
  }
</script>

{#if show}
  <div
    transition:fly={{
      duration: 400,
      x: 220,
      easing: circIn,
    }}
    on:click={click}
  >
    <h3>{title}</h3>
    <p>{message}</p>
  </div>
{/if}

<style>
  div {
    position: fixed;
    top: 0;
    right: 0;
    max-width: 400px;
    padding: 1rem;
    background-color: var(--button-base);
    border-radius: 0.25rem;
    margin: 1rem;
    transition: background-color 200ms ease;
  }
  div:hover {
    background-color: var(--button-hover);
  }
  h3 {
    font-size: 1.1rem;
    margin-top: 0.2rem;
  }
  /* div {
    position: absolute;
    max-width: 200px;
    top: 5%;
    right: 100%;
    padding: 1rem;
  } */
</style>
