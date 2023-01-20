<script>
	import MeetupItem from './MeetupItem.svelte';

	export let meetUps;
</script>

<section id="meetup">
	{#each meetUps as meetup}
		<MeetupItem
			id={meetup.id}
			title={meetup.title}
			subtitle={meetup.subtitle}
			imageUrl={meetup.image}
			address={meetup.address}
			email={meetup.contactEmail}
			description={meetup.description}
			isFav={meetup.isFavorite}
			on:togglefavorite
		/>
	{/each}
</section>

<style>
	section {
		width: 100%;
		display: grid;
		grid-template-columns: 1fr;
		gap: 1rem;
	}

	@media (min-width: 768px) {
		section {
			grid-template-columns: repeat(2, 1fr);
		}
	}
</style>
