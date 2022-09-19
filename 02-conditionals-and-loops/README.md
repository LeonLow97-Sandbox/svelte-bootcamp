### If statements

```svelte
{#if formState === "done"}
<ContactCard userName={name} jobTitle={title} {description} userImage={image} />
{/if}
{#if formState === "invalid"}
<p>Invalid Input</p>
{/if}
```

### else if

```svelte
{#if formState === "done"}
<ContactCard userName={name} jobTitle={title} {description} userImage={image} />
{:else if formState === "invalid"}
<p>Invalid Input</p>
{/if}
```

### each

- `createdContacts` is an array
- The code below adds the latest javascript object into the last element of the new array `createdContacts`

```svelte
    createdContacts = [...createdContacts, 
    {
      name: name, 
      jobTitle: title, 
      imageURL: image, 
      desc: description
    }
  ];
```

```svelte
{#each createdContacts as contact}
<ContactCard 
userName={contact.name} 
jobTitle={contact.jobTitle} 
description={contact.description} 
userImage={contact.imageURL} />
{/each}
```

### Adding an index in `each`

```svelte
{#each createdContacts as contact, index}
<h2># {index + 1}</h2>
<ContactCard 
userName={contact.name} 
jobTitle={contact.jobTitle} 
description={contact.desc} 
userImage={contact.imageURL} />
{:else}
  <p>Please start adding some contacts, we found none!</p>
{/each}
```

### Deleting cards 

```svelte
  function deleteFirst() {
    createdContacts = createdContacts.slice(1)
  }

  function deleteLast() {
    createdContacts = createdContacts.slice(0, -1)
  }
```

### Adding an id to `each`

```svelte
<script>
        createdContacts = [...createdContacts, 
    {
      id: Math.random(),
      name: name, 
      jobTitle: title, 
      imageURL: image, 
      desc: description
    }
</script>

{#each createdContacts as contact, index (contact.id)}
<h2># {index + 1}</h2>
<ContactCard 
userName={contact.name} 
jobTitle={contact.jobTitle} 
description={contact.desc} 
userImage={contact.imageURL} />
{:else}
  <p>Please start adding some contacts, we found none!</p>
{/each}
```

### Reacting to clicks on items

- `on:click="{() => clickHandlerFunc(yourArgument)}"`
- `on:click="{() => clickHandlerFunc.bind(this, yourArgument)}"`

```svelte
  <ul>
	{#each passwords as pw, i}
	  <li on:click={removePassword.bind(this, i)}>{pw}</li>
	{/each}
  </ul>
```

- To remove an item from a list, can use the `filter()` method on the existing array to filter out (=remove) an element with a specific index.
  - `filter(function(element, index, array))`
  - `index` is the index of the current element being processed in the array.

```svelte
	function removePassword(index) {
	  passwords = passwords.filter((pw, idx) => {
		return idx !== index;
	  });
	}
```

- adding an index in the `each` statement increases the performance.



