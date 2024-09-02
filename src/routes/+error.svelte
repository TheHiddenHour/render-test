<script lang="ts">
	import { onMount } from 'svelte';
	import {page} from '$app/stores'

	let imageUrl: string;

	async function getData() {
		const url = 'https://api.thecatapi.com/v1/images/search';
		try {
			const response = await fetch(url);
			if (!response.ok) {
				throw new Error(`Response status: ${response.status}`);
			}

			const json = await response.json();
			imageUrl = json[0]['url'];
		} catch (error: any) {
			throw new Error(error.message);
		}
	}

	onMount(() => {
		getData();
	});
</script>

<div class="grid gap-4 template-rows justify-center justify-items-center h-screen">
	<p class="text-white font-bold text-8xl">{$page.status} :&lpar;</p>
	<p class="text-white">{$page.error?.message}, here's a cat picture</p>
	{#if imageUrl}
		<div class="h-1/2 self-center">
			<img class="h-3/4 object-contain" src={imageUrl} alt="cat" srcset="" />
		</div>
	{/if}
</div>

<style>
	.template-rows {
		grid-template-rows: auto auto 1fr;
	}
</style>
