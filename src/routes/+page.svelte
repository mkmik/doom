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
		console.log(d.getDay(), answer);
	};

	const onKeyPress = (e: any) => {
		if (e.charCode === 13) check();
	};
</script>

<p>What day of the week was: <b>{s}</b> ?</p>

<p><input on:keypress={onKeyPress} bind:value={answer} /></p>

<p><b>{report}</b></p>

{#if report !== ''}
	<p><button on:click={refresh}>Again</button></p>
{/if}
