<script lang="ts">
	import { json } from '@sveltejs/kit';

	let searchTitle: string;
	let searchJson: any = { songs: [] };

	async function fetchSongResults(title: string) {
		const url = `https://api.animethemes.moe/song?include=animethemes.anime&filter[title-like]=%${title}%`;
		const response = await fetch(url);
		if (!response.ok) {
			return {};
		}

		const json = await response.json();
		return json;
	}

	async function searchSong() {
		if (!searchTitle) return;

		searchJson = await fetchSongResults(searchTitle);
		console.log(searchJson);
	}
</script>

<div class="grid template-columns">
	<div>
		<p class="text-white">Top Songs</p>
	</div>
	<div>
		<label class="text-white block" for="songname">Song Name</label>
		<input
			bind:value={searchTitle}
			placeholder="Song name"
			type="text"
			id="songname"
			name="songname"
		/>
		<button
			on:click={searchSong}
			class="px-4 rounded text-white bg-african-violet hover:bg-ultra-violet">Search</button
		>
		<div>
			{#if searchJson.songs.length > 0}
				{#each searchJson.songs as item}
					<p class="text-white">{item.title} | {item.animethemes[0].anime.name}</p>
				{/each}
			{:else}
				<p class="text-white">No search results</p>
			{/if}
		</div>
	</div>
</div>

<style>
	.template-columns {
		grid-template-columns: 1fr 1fr;
	}
</style>
