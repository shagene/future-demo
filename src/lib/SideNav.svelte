<script lang="ts">
	import NavButton from './NavButton.svelte';
	import IconContext from 'phosphor-svelte/lib/IconContext';
	import {
		Horse,
		Question,
		SquaresFour,
		House,
		UsersThree,
		ChartBar,
		Files,
		CirclesThreePlus
	} from 'phosphor-svelte';
</script>

<div class="flex flex-col h-full w-20 bg-gray-800 text-white">
	<div class="p-4 flex justify-center">
		<IconContext values={{ color: '#FFF', size: 32, mirrored: true, weight: 'thin' }}>
			<Horse /></IconContext
		>
	</div>

	<nav class="flex-1">
		<ul class="flex flex-col items-center justify-center py-2 px-4">
			<li><NavButton icon={House} iconType="fill" route="/" routeName="Home" /></li>
			<li>
				<NavButton icon={SquaresFour} iconType="duotone" route="/spaces" routeName="Spaces" />
			</li>
			<li><NavButton icon={UsersThree} iconType="bold" route="/holders" routeName="Holders" /></li>
			<li><NavButton icon={ChartBar} iconType="regular" route="/reports" routeName="Reports" /></li>
			<li><NavButton icon={Files} iconType="light" route="/files" routeName="Files" /></li>
			<li>
				<NavButton
					icon={CirclesThreePlus}
					iconType="thin"
					mirrored="true"
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
