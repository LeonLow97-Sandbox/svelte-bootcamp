<script>
    import Header from "./UI/Header.svelte"
    import MeetupGrid from "./Meetups/MeetupGrid.svelte";
    import TextInput from "./UI/TextInput.svelte"
    import Button from "./UI/Button.svelte"

    let title = ""
    let subtitle = ""
    let address = ""
    let email = ""
    let description = ""
    let imageUrl = ""

    let meetups = [
        {
            id: "m1",
            title: "Coding Bootcamp",
            subtitle: "Learn to code in 2 hours",
            description: "In this meetup, we will have some experts that teach you how to code",
            imageUrl: "https://media-exp1.licdn.com/dms/image/C560BAQHdAaarsO-eyA/company-logo_200_200/0/1595530301220?e=1672876800&v=beta&t=ncZPdETh3EA0MqyUzW9ZOAhbh7gRQpYCItHNF01nXlk",
            address: "27th Nerd Road, 35235 New York",
            contactEmail: "code@test.com"
        },
        {
            id: "m1",
            title: "Swim Together",
            subtitle: "Let\'s go for some swimming",
            description: "I love simming",
            imageUrl: "https://media-exp1.licdn.com/dms/image/C4D0BAQEmT3lq2KZDXw/company-logo_200_200/0/1519856511239?e=1672876800&v=beta&t=s4HJESbFOrf8f2t0JkaHgsfsH9HwGThhjmt3Hgjy1R0",
            address: "27th Hello Road, 35125 New York",
            contactEmail: "swim@test.com"
        }
    ]

    function addMeetUp() {
        const newMeetup = {
            id: Math.random().toString(),
            title: title,
            subtitle: subtitle,
            description: description,
            imageUrl: imageUrl,
            contactEmail: email,
            address: address
        }

        meetups = [newMeetup, ...meetups]
    }
</script>

<style>
    main {
        margin-top: 5rem;
    }

    form {
        width: 30rem;
        max-width: 90%;
        margin: auto;
    }
</style>

<Header />

<main>
    <form on:submit|preventDefault="{addMeetUp}">
        <TextInput id="title" label="Title" type="text" value={title} on:input={(event) => title = event.target.value} />
        <TextInput id="subtitle" type="text" label="Subtitle" value={subtitle} on:input={(event) => subtitle = event.target.value} />
        <TextInput id="address" type="text" label="Address" value={address} on:input={(event) => address = event.target.value} />
        <TextInput id="imageUrl" type="text" label="ImageUrl" value={imageUrl} on:input={(event) => imageUrl = event.target.value} />
        <TextInput id="email" label="E-mail" type="email" value={email} on:input={(event) => email = event.target.value} />
        <TextInput id="description" label="Description" controlType="textarea" value={description} on:input={(event) => description = event.target.value} />
        <Button type="submit" caption="Save" />
    </form>
    <MeetupGrid {meetups} />
</main>





