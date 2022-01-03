<script>
	export let name;
	let count = 0;
	$: doubled = count * 2;

	$: if (count >= 10) {
		alert('count is dangerously high!');
		count = 9;
	}

	function incrementCount() {
		count += 1;
	}

	let numbers = [1, 2, 3, 4];

	function addNumber() {
		numbers[numbers.length] = numbers.length + 1;
	}

	$: sum = numbers.reduce((t, n) => t + n, 0);

	let user = { loggedIn: false };

	function toggle() {
		user.loggedIn = !user.loggedIn;
	}
</script>

<main>
	<h1>Hello {name}!</h1>
	<button on:click={incrementCount}>
		Clicked {count} {count === 1 ? 'time' : 'times'}
	</button>
	<p>{count} doubled is {doubled}</p>

	<p>{numbers.join(' + ')} = {sum}</p>

	<button on:click={addNumber}>
		Add a number
	</button>

	<div>
		{#if user.loggedIn}
		<button on:click={toggle}>
			Log out
		</button>
		{/if}

		{#if !user.loggedIn}
		<button on:click={toggle}>
			Log in
		</button>
		{/if}
	</div>
</main>



<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>