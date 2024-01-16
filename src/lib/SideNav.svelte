<script lang="ts">
	import NavButton from './NavButton.svelte';
	import IconContext from 'phosphor-svelte/lib/IconContext';
	import {
		Question,
		SquaresFour,
		House,
		UsersThree,
		ChartBar,
		Files,
		CirclesThreePlus
	} from 'phosphor-svelte';
	import cslogo from '$lib/images/cs-nav-logo.svg';

</script>

<div class="flex flex-col h-full w-20 bg-gray-800 text-white">
	<div class="p-4 flex justify-center">
		<div class="flex header-item header-content">
			<img class="img w-12 h-12 bg-white rounded-full p-1" src={cslogo} alt="Computershare Logo" />
		</div>
	</div>

	<nav class="flex-1">
		<ul class="flex flex-col items-center justify-center py-2 px-4">
			<li class="pt-2"><NavButton icon={House} iconType="fill" route="/" routeName="Home" /></li>
			<li class="pt-2">
				<NavButton icon={SquaresFour} iconType="duotone" route="/spaces" routeName="Spaces" />
			</li>
			<li class="pt-2"><NavButton icon={UsersThree} iconType="bold" route="/holders" routeName="Holders" /></li>
			<li class="pt-2"><NavButton icon={ChartBar} iconType="regular" route="/reports" routeName="Reports" /></li>
			<li class="pt-2"><NavButton icon={Files} iconType="light" route="/files" routeName="Files" /></li>
			<li class="pt-2">
				<NavButton
					icon={CirclesThreePlus}
					iconType="thin"
					route="/apps"
					routeName="Apps"
				/>
			</li>
		</ul>
	</nav>
	<div. class="p-4 flex justify-center">
		<NavButton icon={Question} iconType="duotone" route="/help" routeName="Help" />
	</div.>
</div>

<style>
</style>
