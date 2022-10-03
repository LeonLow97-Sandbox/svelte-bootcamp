<script>
	import {tick} from 'svelte'
	import App from "../../04-course-project/project-setup/src/App.svelte";
	import Button from "../../04-course-project/project-setup/src/UI/Button.svelte";
	import Product from "./Product.svelte"
	import Modal from "./Modal.svelte"

	let products = [
		{
			id: "p1",
			title: "A book",
			price: 9.99
		}
	]

	let text = "This is some dummy text!"

	let showModal = false;
	let closeable = false;

	function addToCart(event) {
		console.log(event)
		console.log(event.detail)
	}
	function deleteProduct(event) {
		console.log(event.detail)
	}

	function transform(event) {
		if (event.which !== 9) {
			return;
		}
		event.preventDefault();

		const selectionStart = event.target.selectionStart;
		const selectionEnd = event.target.selectionEnd;
		const value = event.target.value;

		text = value.slice(0, selectionStart) + value.slice(selectionStart, selectionEnd).toUpperCase() + 
		value.slice(selectionEnd);

		tick().then(() => {
			// Adjust the text cursor to the same position after selection
			event.target.selectionStart = selectionStart;
			event.target.selectionEnd = selectionEnd
		})

		// Adjust the text cursor to the same position after selection
		// Will not work!
		// event.target.selectionStart = selectionStart;
		// event.target.selectionEnd = selectionEnd
	}
</script>

{#each products as product}
<Product 
	{...product}
	on:add-to-cart={addToCart} 
	on:delete={deleteProduct}
/>
{/each}

<button on:click={() => showModal = true}>Show Modal</button>

{#if showModal}
<Modal 
	on:cancel={() => showModal = false} 
	on:close={() => showModal = false}
	let:didAgree={closeable}>
	<h1 slot="header">Hello!!</h1>
	<p>This works!</p>
	<button slot="footer" on:click={() => showModal = false} disabled={!closeable}>Confirm</button>
</Modal>
{/if}

<textarea cols="" rows="5" value={text} on:keydown={transform} ></textarea>

