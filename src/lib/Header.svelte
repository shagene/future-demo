<script lang="ts">
	// Your script content
	export let isVisible: boolean = true;
  let recognizedText = writable('');
	import { onMount } from 'svelte';
	import { writable } from 'svelte/store';
	import img from '$lib/images/disney.png';
	import {
		MagnifyingGlass,
		BellRinging,
		Calendar,
		Notepad,
		CirclesFour
	} from 'phosphor-svelte';
	import profile from '$lib/images/profile.png';
	import SpeechRecognition from './ SpeechRecognition.svelte';
</script>

<header
  class={`fixed top-0 mt-auto pt-10 w-full flex justify-between items-center transition-transform duration-300 ${isVisible ? '' : '-translate-y-full'}`}
>
	<div class="flex header-item header-content">
		<img class="img w-60 max-h-14" src={img} alt="Disney" />
	</div>
	<div class="search-container h-12">
		<MagnifyingGlass size={24} class="search-icon ml-4" />
		<input class="search-input" type="text" placeholder="Search" />
    <div class="mr-4">
      <SpeechRecognition startIconSize={32} {recognizedText} />
    </div>
		
	</div>

	<div class="header-item header-content">
  <CirclesFour size={32} class="icon mr-4" />
  <Notepad size={32} class="icon mr-4" />
  <Calendar size={32} class="icon mr-4" />
  <BellRinging size={32} class="icon mr-4" />
  <div class="profile-container">
    <img class="img w-11 h-11 rounded-full" src={profile} alt="User Profile" />
    <!-- Last login text will be placed here, aligned to the right under the profile image -->
    <!-- <div class="last-login">
      Last login<br>
      1/10/23, 7:09pm
    </div> -->
  </div>
</div>

<!-- Put last log in here and move to the right so its under the profile logo -->

</header>

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

  .profile-container {
    display: flex;
    flex-direction: column;
    align-items: center; /* Center the items horizontally */
    justify-content: center; /* Center the items vertically */
  }

  .last-login {
    text-align: center;
    font-size: 0.75rem; /* Adjust the font size as needed */
    color: #333; /* Adjust the text color as needed */
    margin-top: 0.25rem; /* Adjust the margin as needed */
  }

  .icon {
    pointer-events: all;
  }

</style>
