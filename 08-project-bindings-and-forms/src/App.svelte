<script>
    import Header from "./UI/Header.svelte"
    import MeetupGrid from "./Meetups/MeetupGrid.svelte";
    import TextInput from "./UI/TextInput.svelte"
    import Button from "./UI/Button.svelte"
    import EditMeetup from "./Meetups/EditMeetup.svelte"

    let meetups = [
        {
            id: "m1",
            title: "Coding Bootcamp",
            subtitle: "Learn to code in 2 hours",
            description: "In this meetup, we will have some experts that teach you how to code",
            imageUrl: "https://media-exp1.licdn.com/dms/image/C560BAQHdAaarsO-eyA/company-logo_200_200/0/1595530301220?e=1672876800&v=beta&t=ncZPdETh3EA0MqyUzW9ZOAhbh7gRQpYCItHNF01nXlk",
            address: "27th Amos Road, 35235 New York",
            contactEmail: "code@test.com",
            isFavourite: false
        },
        {
            id: "m2",
            title: "Swim Together",
            subtitle: "Let\'s go for some swimming",
            description: "I love simming",
            imageUrl: "https://media-exp1.licdn.com/dms/image/C4D0BAQEmT3lq2KZDXw/company-logo_200_200/0/1519856511239?e=1672876800&v=beta&t=s4HJESbFOrf8f2t0JkaHgsfsH9HwGThhjmt3Hgjy1R0",
            address: "27th Hello Road, 35125 New York",
            contactEmail: "swim@test.com",
            isFavourite: false
        }
    ]

    let editMode = null;

    function addMeetUp(event) {
        const newMeetup = {
            id: Math.random().toString(),
            title: event.detail.title,
            subtitle: event.detail.subtitle,
            description: event.detail.description,
            imageUrl: event.detail.imageUrl,
            contactEmail: event.detail.email,
            address: event.detail.address
        }

        meetups = [newMeetup, ...meetups]
        editMode = null;
    }

    function cancelEdit() {
        editMode = null
    }

    function toggleFavourite(event) {
        const id = event.detail;
        // returns a single meetup object if true/found
        const updatedMeetup = {...meetups.find(m => m.id === id)}
        updatedMeetup.isFavourite = !updatedMeetup.isFavourite
        const meetupIndex = meetups.findIndex(m => m.id === id)
        // copy the original array
        const updatedMeetups = [...meetups]
        // replace the isFavourite in the index of the array
        updatedMeetups[meetupIndex] = updatedMeetup
        // override the original array
        meetups = updatedMeetups
    }
</script>

<style>
    main {
        margin-top: 5rem;
    }

    .meetup-controls {
        margin: 1rem;

    }
</style>

<Header />

<main>
    <div class="meetup-controls" >
        <Button on:click={() => editMode = 'add'}>New Meetup</Button>
    </div>
    
    {#if editMode === "add"}
        <EditMeetup on:save={addMeetUp} on:cancel={cancelEdit} />
    {/if}
    <MeetupGrid {meetups} on:togglefavourite={toggleFavourite} />
</main>





