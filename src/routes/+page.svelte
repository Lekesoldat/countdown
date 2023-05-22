<script>
	import { onMount } from 'svelte';

	/** @type {Date} */
	const targetDate = new Date('June 12, 2023');


	/** @type {number} */
	let totalSeconds = Math.floor((targetDate.getTime() - new Date().getTime()) / 1000);

	/** @type {number | null} */
	let interval = null;

	onMount(() => {
		function updateCountdown() {
			totalSeconds = Math.floor((targetDate.getTime() - new Date().getTime()) / 1000);
		}

		interval = setInterval(updateCountdown, 1000);

		return () => {
			if (interval !== null) {
				clearInterval(interval);
			}
		};
	});

	/** @type {number} */
	let days;
	/** @type {number} */
	let hours;
	/** @type {number} */
	let minutes;
	/** @type {number} */
	let seconds;
	/** @type {number} */
	let totalHours;
	/** @type {number} */
	let totalMinutes;

	$: days = Math.floor(totalSeconds / 60 / 60 / 24);
	$: hours = Math.floor((totalSeconds / 60 / 60) % 24);
	$: minutes = Math.floor((totalSeconds / 60) % 60);
	$: seconds = totalSeconds % 60;
	$: totalHours = Math.floor(totalSeconds / 60 / 60);
	$: totalMinutes = Math.floor(totalSeconds / 60);
</script>

<main>
	<h1>{days} dager, {hours} timer</h1>
	<h2>{totalHours} timer, {minutes} minutter</h2>
	<h3>{totalMinutes} minutter, {seconds} sekunder</h3>
	<p>... igjen til innlevering 12. juni 👺</p>
</main>

<style>
	main {
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
		height: 100vh;
		text-align: center;
		font-family: Arial, sans-serif;
	}
</style>
