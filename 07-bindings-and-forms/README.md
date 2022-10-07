# Bindings and Forms

## 2-way binding refresher

- If you have a variable value instead of "val", could use shorthand notation `bind:value` instead of `bind:value={value}`.

## Custom Input

- CustomInput.svelte

```js
<script>
    export let val;
</script>

<input type="text" bind:value={val}>
```

- App.svelte
- In `<CustomInput bind:val={val} />`, the first `val` refers to that in `CustomInput.svelte` and the second {val} refers to that in `App.svelte`.

```js
<script>
    import CustomInput from "./CustomInput.svelte"
    let val = 'Max'

    $: console.log(val)

    function setValue(event) {
        val = event.target.value
    }
</script>

<CustomInput bind:val={val} />
```

## Custom Component Binding

- Not recommended.

- Toggle.svelte

```js
<script>
    export let chosenOption = 1
</script>

<button
    disabled={chosenOption == 1}
    on:click={() => chosenOption = 1}>Option 1
</button>
<button
    disabled={chosenOption == 2}
    on:click={() => chosenOption = 2}>Option 2
</button>
```

- App.svelte

```js
<script>
    let selectedOption = 1
</script>

<Toggle bind:chosenOption={selectedOption} />
```

## Checkbox

```js
<label>
  <input type="checkbox" bind:checked={agreed} />
  Agree to terms?
</label>
```

## Radio Button

```js
<label>
    <input type="radio" name="color" value="red" bind:group={favColor}>
    Red
</label>
<label>
    <input type="radio" name="color" value="green" bind:group={favColor}>
    Green
</label>
<label>
    <input type="radio" name="color" value="blue" bind:group={favColor}>
    Blue
</label>
```
