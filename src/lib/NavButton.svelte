<script lang="ts">
    import type { SvelteComponent } from 'svelte';
    export let icon: typeof SvelteComponent;
    export let route: string;
    export let routeName: string;
    export let iconType: string;
    import { page } from '$app/stores';
    import { get } from 'svelte/store';
    import { browser } from '$app/environment';
</script>

<div class="h-13">
    <button
      class="btn btn-square min-h-8 h-8 w-14 {get(page).url.pathname === route ? 'active-route' : 'inactive-route'}"
      on:click={() => browser && (window.location.href = route)}
    >
        <svelte:component this={icon} weight={iconType} class="h-6 w-6" style="color: {get(page).url.pathname === route ? '#93186C' : '#FFFFFF'}" />
    </button>
    <span class="flex flex-col items-center">{routeName}</span>
</div>

<style>
    .btn {
    transition: box-shadow 0.3s, background-color 0.3s;
  }

  .btn:hover {
    box-shadow: 0 0 10px rgba(147, 24, 108, 0.5); /* Adjust color and intensity as needed */
    background-color: rgba(255, 255, 255, 0.2); /* Lighter background color on hover */ 
  }
    .active-route {
        background-color: #FFFFFF;
        border-color: #93186c;
    }
    .inactive-route {
        background-color: transparent;
        border-color: transparent;
    }
</style>