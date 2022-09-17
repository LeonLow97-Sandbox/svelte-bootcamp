<script>
	import ContactCard from './ContactCard.svelte'

	let name = "Leon";
	let age = 25;

	// let uppercaseName; not required!
	// "$:" works only in JavaScript
	// dynamic value
	$: uppercaseName = name.toUpperCase();

	$: console.log(name)

	$: if (name === "Bryan") {
		age = 70000
	}

	function incrementAge() {
		age += 1;
	}

	function changeName() {
		console.log("It runs!")
		name = "Bryan"
	}

	function nameInput(event) {
		const enteredValue = event.target.value;
		name = enteredValue;
	}
</script>

<style>
	h1 {
		color: mediumseagreen;
	}
</style>

<h1>Hello {uppercaseName}! My age is {age}!</h1>
<button on:click="{incrementAge}">Change Age</button>
<!-- <button on:click="{changeName}" >Change Name</button> -->
<!-- <input type="text" value="{name}" on:input="{nameInput}" /> -->
<input type="text" bind:value="{name}" />
<h1>Hi</h1>