## Forwarding Events

- Parent file

```js
// App.svelte
<script>
	import Product from "./Product.svelte"
</script>

<Product productTitle="A Book" on:click={() => alert("Clicked!")} />
```

- Child (forward an event `on:click`)

```js
<script>
    export let productTitle
</script>

<article>
    <h1>{productTitle}</h1>
    <button on:click>Add to Card</button>
    <button>Delete</button>
</article>
```

## Custom Events

- In parent (App.ssvelte)
- Passing elements from child to parent using event.detail.

```js
<script>
	import Product from "./Product.svelte"

	function addToCart(event) {
		console.log(event.detail) // {id: 'p1'}
	}
	function deleteProduct(event) {
		console.log(event.detail)	// p1
	}
</script>

<Product
	productTitle="A Book"
	on:add-to-cart={addToCart}
	on:delete={deleteProduct}
/>
```

- In child (Product.svelte)
- `import {createEventDispatcher} from "svelte"`
- `dispatch()` takes 2 parameters (event, any value)

```js
<script>
    import {createEventDispatcher} from "svelte"

    export let productTitle

    const dispatch = createEventDispatcher()

    function addToCart() {
        dispatch('add-to-cart', {id: 'p1'})
    }
</script>

<article>
    <h1>{productTitle}</h1>
    <button on:click={addToCart}>Add to Card</button>
    <button on:click={() => {dispatch('delete', 'p1')}} >Delete</button>
</article>
```

## Spreading Props

- props must have the same name in parent and child component.

```js
{#each products as product}
<Product
	{...product}
	on:add-to-cart={addToCart}
	on:delete={deleteProduct}
/>
{/each}
```

## Slots

- Modal.svelte

```js
<div class="backdrop"></div>
<div class="modal">
  <header>
    <slot name="header" />
  </header>
  <div class="content">
    <slot />
  </div>
  <footer>
    <slot name="footer">
      <button>Close</button>
    </slot>
  </footer>
</div>
```

- App.svelte

```js
<Modal>
  <h1 slot="header">Hello!!</h1>
  <p>This works!</p>
  <button slot="footer">Confirm</button>
</Modal>
```

## Using Slot Props (Passing props up to the parent component)

- In Modal.svelte

```js
<footer>
  <slot name="footer" didAgree={agreed}>
    <button on:click={() => dispatch("close")} disabled={!agreed}>
      Close
    </button>
  </slot>
</footer>
```

- In App.svelte
- Syntax: `let:didAgree={closeable}` where `closeable` is defined in App.svelte.

```js
<Modal
  on:cancel={() => (showModal = false)}
  on:close={() => (showModal = false)}
  let:didAgree={closeable}
>
  <h1 slot="header">Hello!!</h1>
  <p>This works!</p>
  <button
    slot="footer"
    on:click={() => (showModal = false)}
    disabled={!closeable}
  >
    Confirm
  </button>
</Modal>
```

## The component lifecycle

- Creation

  - <script> Executes
    - Basic initialization work
  - `onMount()`
    - More complex init work (e.g., data fetching)
    - Runs after entire script is ran and components are displayed on browser.
    - `import {onMount, onDestroy} from "svelte"`
  - `onDestroy()`
    - Cleanup work

- Updates
  - `beforeUpdate()`
    - Save (DOM) state before Svelte updates it
  - `afterUpdate()`
    - Manually update DOM/view after Svelte update.
  - `tick()` (rarely used)
    - Await Svelte's DOM update.
    - `tick().then(() => {})` used when you want to update something after all the scheduled tasks have been completed.

- `beforeUpdate()` and `afterUpdate()` usually used for auto scrolling.
