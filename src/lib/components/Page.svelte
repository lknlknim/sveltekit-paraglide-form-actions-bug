<script lang="ts">
	import type { SubmitFunction } from '@sveltejs/kit';
	import { enhance } from '$app/forms';
	import { goto } from '$app/navigation';
	import { page } from '$app/stores';

	export let action = '?/update';

	const go = () => goto(new URL($page.url).pathname.replace('create', '123'));

	const submit: SubmitFunction = () => {
		return ({ result }) => {
			if (result.type === 'success') {
				go();
			}
		};
	};
</script>

<form method="post" {action} use:enhance={submit}>
	<button>{$page.params.productId === 'create' ? 'Create' : 'Update'}</button>
</form>

<button on:click={go}>goto</button>
