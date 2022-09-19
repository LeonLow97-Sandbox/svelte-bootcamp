### Event Identifier

- only allow the button to be used once
- `<button on:click|once={addContact} >Add Contact Card</button>`

- `<button on:click|stopPropagation={addContact} >Add Contact Card</button>`

- `<button on:click|preventDefault={addContact} >Add Contact Card</button>`
    - used in "forms"
    - prevent browser default refresh

### Inline functions

```svelte
<button on:click="{(event) => {createdContacts = createdContacts.slice()}}">Delete First</button>
```