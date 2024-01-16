<script lang="ts">
	// Your script content
</script>

<footer class="mt-auto h-14 w-full flex justify-between items-center">
	<div class="flex footer-content">
		<div class="footer-item">Terms & Conditions</div>
		<div class="footer-item">Privacy Policy</div>
	</div>
	<div class="footer-item footer-content">©2023 Computershare Limited. All rights reserved.</div>
</footer>

<style>
	footer {
		position: relative;
		padding-left: 3rem;
		padding-right: 3rem;
	}

	footer::before {
		content: '';
		position: absolute;
		top: 0;
		left: 50%;
		width: calc(100% - 6rem);
		transform: translateX(-50%);
		border-top: 1px solid #AFAFAF;
	}

	.footer-content {
		position: relative;
		z-index: 1; /* Ensure content is above the pseudo-element */
	}

	.footer-item {
		color: #333;
		font-family: Overpass, sans-serif;
		font-size: 14px;
		font-style: normal;
		font-weight: 600;
		line-height: normal;
		margin-right: 1rem; /* Adjust spacing between items if needed */
	}

	/* Remove margin from the last item */
	.footer-item:last-child {
		margin-right: 0;
	}
</style>