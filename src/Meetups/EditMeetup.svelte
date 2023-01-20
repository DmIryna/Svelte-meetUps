<script>
	import { createEventDispatcher } from 'svelte';
	import Button from '../UI/Button.svelte';
	import Modal from '../UI/Modal.svelte';
	import TextInput from '../UI/TextInput.svelte';
	import { isEmpty, isValidEmail } from '../helpers/validation';

	let title = '';
	let titleValid = false;
	let subtitle = '';
	let subtitleValid = false;
	let address = '';
	let addressValid = false;
	let email = '';
	let emailValid = false;
	let description = '';
	let descriptionValid = false;
	let imageUrl = '';
	let imageUrlValid = false;
	let formIsValid = false;

	$: titleValid = !isEmpty(title);
	$: subtitleValid = !isEmpty(subtitle);
	$: addressValid = !isEmpty(address);
	$: emailValid = isValidEmail(email);
	$: descriptionValid = !isEmpty(description);
	$: imageUrlValid = !isEmpty(imageUrl);
	$: formIsValid =
		titleValid && subtitleValid && addressValid && emailValid && descriptionValid && imageUrlValid;

	const dispatch = createEventDispatcher();

	const submitForm = function () {
		dispatch('save', {
			title: title,
			subtitle: subtitle,
			address: address,
			email: email,
			description: description,
			imageUrl: imageUrl
		});
	};

	const cancel = function () {
		dispatch('cancel');
	};
</script>

<section>
	<Modal title="Edit meetup data" on:cancel>
		<form on:submit|preventDefault={submitForm}>
			<TextInput
				label={'Title'}
				id={'title'}
				value={title}
				type={'text'}
				valid={titleValid}
				validityMessage={'Please enter a valid title.'}
				on:input={(event) => (title = event.target.value)}
			/>
			<TextInput
				label={'Subtitle'}
				id={'subtitle'}
				value={subtitle}
				type={'text'}
				valid={subtitleValid}
				validityMessage={'Please enter a valid subtitle.'}
				on:input={(event) => (subtitle = event.target.value)}
			/>
			<TextInput
				label={'Address'}
				id={'address'}
				value={address}
				type={'text'}
				valid={addressValid}
				validityMessage={'Please enter a valid address.'}
				on:input={(event) => (address = event.target.value)}
			/>
			<TextInput
				label={'E-mail'}
				id={'email'}
				value={email}
				type={'email'}
				valid={emailValid}
				validityMessage={'Please enter a valid email.'}
				on:input={(event) => (email = event.target.value)}
			/>
			<TextInput
				label={'Image URL'}
				id={'imageUrl'}
				value={imageUrl}
				type={'text'}
				valid={imageUrlValid}
				validityMessage={'Please enter a valid imageUrl.'}
				on:input={(event) => (imageUrl = event.target.value)}
			/>
			<TextInput
				label={'Description'}
				id={'description'}
				value={description}
				controlType={'text-area'}
				valid={descriptionValid}
				validityMessage={'Please enter a valid description.'}
				on:input={(event) => (description = event.target.value)}
			/>
		</form>
		<div slot="footer">
			<Button type="button" mode="outline" on:click={cancel}>Close</Button>
			<Button type="button" on:click={submitForm} disabled={!formIsValid}>Save</Button>
		</div>
	</Modal>
</section>

<style>
	form {
		width: 100%;
	}
</style>
