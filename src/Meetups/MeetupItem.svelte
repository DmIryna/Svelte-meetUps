<script>
	import Button from '../UI/Button.svelte';
	import Badge from '../UI/Badge.svelte';
	import { createEventDispatcher } from 'svelte';

	export let title;
	export let subtitle;
	export let imageUrl;
	export let description;
	export let address;
	export let email;
	export let id;
	export let isFav;

	const dispatch = createEventDispatcher();
</script>

<article>
	<header>
		<h1>
			{title}
			{#if isFav}
				<Badge>FAVORITE</Badge>
			{/if}
		</h1>
		<h2>{subtitle}</h2>
	</header>
	<div class="image">
		<img src={imageUrl} alt={title} />
	</div>
	<div class="content">
		<p>{description}</p>
	</div>
	<footer>
		<Button href="mailto:{email}">Contacts</Button>

		<Button
			mode="outline"
			color={isFav ? null : 'success'}
			type="button"
			on:click={() => dispatch('togglefavorite', id)}>{isFav ? 'Unfavorite' : 'Favorite'}</Button
		>

		<Button type="button">Show details</Button>
	</footer>
</article>

<style>
	article {
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		border-radius: 5px;
		background-color: white;
		margin: 1rem;
	}

	header,
	.content,
	footer {
		padding: 1rem;
	}

	.imgage {
		width: 100;
		height: 14rem;
	}

	.image img {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}

	h1 {
		font-size: 1.25rem;
		margin: 0.5rem 0;
	}

	h1.is-favorite {
		color: white;
		background-color: rgb(6, 134, 134);
		padding: 0 0.5rem;
		border-radius: 5px;
	}

	h2 {
		font-size: 1rem;
		color: #808080;
		margin: 0.5rem 0;
	}

	p {
		font-size: 1.25rem;
		margin: 0;
	}

	div {
		text-align: right;
	}

	.content {
		height: 4rem;
	}
</style>
