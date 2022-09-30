<script>
	import ContactCard from './ContactCard.svelte'
	import Assignment1 from "./Assignment1.svelte"

	let name = "";
	let title = "";
	let description = "";
	let image = "";
	let age = 25;

	// for assignment 1
	// let goal = "";

	// let uppercaseName; not required!
	// "$:" works only in JavaScript
	// dynamic value (label)
	// when name changes, the uppercase will be triggered
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
<input type="text" bind:value="{title}" />
<input type="text" bind:value="{image}" />
<textarea rows="3" bind:value={description} ></textarea>

<ContactCard 
userName="{name}" 
jobTitle={title} 
{description}
userImage={image} />

<!-- <Assignment1 courseGoal={goal} /> -->
<!-- <input type="text" placeholder="Course Goal" bind:value={goal} /> -->