<script>
	import Header from '../UI/Header.svelte';
	// import MeetupItem from "../Meetups/MeetupItem.svelte"
	import MeetupGrid from '../Meetups/MeetupGrid.svelte';
	import Button from '../UI/Button.svelte';
	import EditMeetup from '../Meetups/EditMeetup.svelte';
	import TextInput from '../UI/TextInput.svelte';

	let meetUps = [
		{
			id: `m1`,
			title: `Concert`,
			subtitle: `Let's meet in a concert-holl`,
			description: `Meeting with friends, listetning to a cool music`,
			address: `Kyiv, Concert-Hall`,
			contactEmail: `concert_hall@test.com`,
			image: `https://images.unsplash.com/photo-1429962714451-bb934ecdc4ec`,
			isFavorite: false
		},
		{
			id: `m2`,
			title: `Yoga`,
			subtitle: `Do yoga with me`,
			description: `Take time for your body and enjoy your it`,
			address: `Kyiv, Tyraspilska, 58`,
			contactEmail: `yoga@test.com`,
			image: `https://images.unsplash.com/photo-1544367567-0f2fcb009e0b`,
			isFavorite: false
		}
	];

	const addMeetup = function (event) {
		const newMeetUp = {
			id: Math.random().toString(),
			title: event.detail.title,
			subtitle: event.detail.subtitle,
			description: event.detail.description,
			address: event.detail.address,
			contactEmail: event.detail.email,
			image: event.detail.imageUrl
		};

		meetUps = [newMeetUp, ...meetUps];
		editMode = null;
	};
	const toggleFavorite = function (event) {
		const id = event.detail;
		const updatedMeetUp = { ...meetUps.find((m) => m.id === id) };
		updatedMeetUp.isFavorite = !updatedMeetUp.isFavorite;
		const meetupIndex = meetUps.findIndex((m) => m.id === id);
		const updatedMeetUps = [...meetUps];
		updatedMeetUps[meetupIndex] = updatedMeetUp;
		meetUps = updatedMeetUps;
	};

	let editMode;

	const cancelEdit = function () {
		editMode = null;
	};
</script>

<Header />

<main id="meetup">
	<div class="meetup-controls">
		<Button on:click={() => (editMode = 'add')}>New meetup</Button>
	</div>
	{#if editMode === 'add'}
		<EditMeetup on:save={addMeetup} on:cancel={cancelEdit} />
	{/if}
	<!-- left-side meetUps - is a component from each loop on MeetupGrid page, right-side - refers to our array -->
	<MeetupGrid {meetUps} on:togglefavorite={toggleFavorite} />
</main>

<style>
	#meetup {
		margin-top: 5rem;
	}

	.meetup-controls {
		margin: 1rem;
	}
</style>
