<script lang="ts">
	let answer = '';
	let report = '';
	let d: Date;
	let s = '';

	let dow = ['sunday', 'monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday'];

	const randomDate = (start: Date, end: Date) => {
		return new Date(start.getTime() + Math.random() * (end.getTime() - start.getTime()));
	};
	const refresh = () => {
		d = randomDate(new Date(1700, 0, 1), new Date(2200, 0, 1));
		s = d.toJSON().slice(0, 10);
		answer = '';
		report = '';
	};
	refresh();

	const check = () => {
		let index = dow.indexOf(answer.toLowerCase().trim());
		if (index == d.getDay()) {
			report = 'Correct!';
		} else {
			report = 'Wrong!';
		}
	};

	const verify = (node: any) => {
		const onKeyPress = (e: any) => {
			if (e.charCode === 13) {
				check();
				node.blur();
			}
		};
		node.addEventListener('keypress', onKeyPress);

		return {
			destroy() {
				node.removeEventListener('keypress', onKeyPress);
			}
		};
	};
</script>

<div class="h-screen grid gap-4 place-items-center text-xl">
	<div>What day of the week was: <b>{s}</b> ?</div>

	<div>
		<input class="border border-sky-500 rounded-md p-2" use:verify bind:value={answer} />
	</div>

	<div class="h-8"><b>{report}</b></div>

	<div class="h-8">
		{#if report !== ''}
			<button
				class="font-bold py-1 px-4 rounded bg-blue-500 text-white hover:bg-blue-700"
				on:click={refresh}>Again</button
			>
		{/if}
	</div>
</div>
