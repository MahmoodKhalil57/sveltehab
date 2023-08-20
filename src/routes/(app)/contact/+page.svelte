<script lang="ts">
	import type { PageData, ActionData } from './$types';
	import FormBuilder from '$lib/components/form/formBuilder.svelte';
	import { settings } from '$lib/utils/settings';
	import { apiStructure } from '$lib/utils/apiStructure';
	import { enhance } from '$app/forms';
	import FormError from '$lib/components/ui/formError.svelte';
	import toast from 'svelte-french-toast';

	const formStructure = apiStructure.contact.contactForm.formStructure;

	// export let data: PageData;
	export let form: ActionData;

	const toastError = (message: string) => {
		toast.error(message, {
			position: 'bottom-right',
			style: 'background-color: hsl(var(--sc)); color: var(--sf);text-align:center'
		});
	};
	$: if (form?.errorMessage) {
		toastError(form.errorMessage);
	}
</script>

<div class="flex-col gap-6 px-2 prose sm:pb-40 flex-center stretch">
	<h2 class="m-0">Contact me</h2>
	<p class="px-6 m-0">
		You can contact me by sending an email to <a
			href="mailto:{settings.email}"
			class="link link-primary">{settings.email}</a
		>
		or by sending me a message using the following form.
	</p>
	<form
		id="contact"
		class="flex-col w-full max-w-xl gap-3 px-10 flex-center text-start"
		method="POST"
		use:enhance
	>
		<FormBuilder {formStructure} />

		<button class="mt-10 btn btn-primary btn-wide">Submit</button>
	</form>
</div>
