<script lang="ts">
	// Your script content
	export let isVisible: boolean = true;
	import { onMount } from 'svelte';
  import { writable } from 'svelte/store';
  import img from '$lib/images/disney.png';
  import { Microphone, MagnifyingGlass } from 'phosphor-svelte';

  let speechRecognition: any;
  let isListening = writable(false);
  let recognizedText = writable('');

  onMount(() => {
    const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    if (SpeechRecognition) {
      speechRecognition = new SpeechRecognition();
      speechRecognition.continuous = true;
      speechRecognition.interimResults = true;
      speechRecognition.onresult = (event: any) => {
        let transcript = '';
        for (let i = event.resultIndex; i < event.results.length; ++i) {
          transcript += event.results[i][0].transcript;
        }
        recognizedText.set(transcript.trim());
      };
      speechRecognition.onerror = (event: any) => {
        console.error('Speech Recognition Error:', event.error);
      };
    } else {
      console.error('Speech Recognition API not supported in this browser.');
    }
  });

  function startListening() {
    if (speechRecognition) {
      speechRecognition.start();
      isListening.set(true);
    }
  }

  function stopListening() {
    if (speechRecognition) {
      speechRecognition.stop();
      isListening.set(false);
    }
  }
</script>

<header
	class={`fixed top-0 mt-auto pt-10 w-full flex justify-between items-center transition-transform duration-300 ${isVisible ? '' : '-translate-y-full'}`}
>
	<div class="flex header-item header-content">
		<img class="img w-60 max-h-14" src={img} alt="Disney" />
	</div>
	<div class="search-container h-12">
    <MagnifyingGlass size="{24}" class="search-icon ml-4" />
    <input class="search-input" type="text" placeholder="Search" />
    <button on:click={startListening} class="microphone-button">
      <Microphone size="{32}" class="search-icon mr-4" />
    </button>
  </div>

	<div class="header-item header-content">Profile Icon</div>
</header>

{#if $isListening}
  <div class="speech-popup">
    <p>Listening...</p>
    <p>{$recognizedText}</p>
    <button on:click={stopListening}>Stop</button>
  </div>
{/if}


<style>
	header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		position: fixed;
		top: 0;
		left: 5rem; /* Align the left edge with the sidebar */
		width: calc(100% - 5rem); /* Subtract the width of the sidebar */
		padding: 1rem 3rem; /* Adjusted padding for top and bottom */
		transition: transform 0.3s;
		z-index: 10; /* Ensure the header is above other content */
	}

	.header-item,
	.search-container {
		flex: 1; /* Distribute space evenly */
		display: flex;
		justify-content: center; /* Center content horizontally */
		align-items: center; /* Center content vertically */
	}

	.header-item:first-child,
	.header-item:last-child {
		justify-content: flex-start; /* Align the first item to the start */
	}

	.header-item:last-child {
		justify-content: flex-end; /* Align the last item to the end */
		margin-right: 0;
	}

	.search-container {
		position: relative;
		border-radius: 30px;
		border: 1px solid #afafaf;
	}

	.search-icon {
		position: absolute;
		left: 10px;
	}

	.search-input {
		width: 100%;
		padding-left: 40px; /* Make padding at least the width of the icon */
		text-align: center;
		border: none;
		background: inherit; /* Use the same background color as the container */
		color: inherit; /* Use the same font color as the container */
	}

  .speech-popup {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: white;
    padding: 1rem;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    z-index: 20; /* Above the header */
  }

  .microphone-button {
    background: none;
    border: none;
    padding: 0;
    cursor: pointer;
  }

  /* Ensure the microphone icon is clickable */
  .search-icon {
    pointer-events: all;
  }
</style>
