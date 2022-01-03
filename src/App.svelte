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

	//if else
	let user = { loggedIn: false };

	function toggle() {
		user.loggedIn = !user.loggedIn;
	}

	//each loop
	let cats = [
		{ id: 'J---aiyznGQ', name: 'Keyboard Cat' },
		{ id: 'z_AbfPXTKms', name: 'Maru' },
		{ id: 'OUtn3pvWmpg', name: 'Henri The Existential Cat' }
	];

	//DOM events
	let m = { x: 0, y: 0 };

	function handleMousemove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}

	let input_name = 'world';
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

	<!--if else-->
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

	<input bind:value={input_name}>

	<h3>Hello {input_name}!</h3>
	
</main>

<!-- each loop -->
<h2>The Famous Cats of YouTube</h2>
<ul>
	{#each cats as cat, i}
		<li><a target="_blank" href="https://www.youtube.com/watch?v={cat.id}">
			{i+1}: {cat.name}
		</a></li>
	{/each}
</ul>

<div on:mousemove={handleMousemove} style="width:100%; height:100%;">
	The mouse position is {m.x} x {m.y}
</div>

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