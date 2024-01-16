<!-- SpeechRecognition.svelte -->
<script lang="ts">
	import { onMount } from 'svelte';
	import { writable } from 'svelte/store';
	import { Microphone } from 'phosphor-svelte';

	export let startIconSize: number = 32;
	export let recognizedText = writable('');

	let speechRecognition: any;
	let isListening = writable(false);

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

<button on:click={startListening} class="microphone-button">
    <div class="microphone-icon">
        <Microphone size={startIconSize} />
      </div>
</button>

{#if $isListening}
	<div class="speech-popup">
		<p>Listening...</p>
		<p>{$recognizedText}</p>
		<button on:click={stopListening}>Stop</button>
	</div>
{/if}

<style>
	.microphone-button {
		background: none;
		border: none;
		padding: 0;
		cursor: pointer;
        display: block;
	}

	.microphone-icon {
		pointer-events: all;
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
</style>
