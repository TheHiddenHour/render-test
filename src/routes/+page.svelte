<script lang="ts">
	let songTitle: string;
	let songsJson: any;

	async function searchSong(title: string) {
		if (!title) return;

		const url = `https://api.animethemes.moe/song?include=animethemes.anime&filter[title-like]=%${title}%`;
		try {
			const response = await fetch(url);
			if (!response.ok) {
				console.log(`Response status: ${response.status}`);
				return;
			}

			const json = await response.json();
			console.log(json);
			songsJson = json;
		} catch (error: any) {
			console.error(error.message);
		}
	}
</script>

<input
	bind:value={songTitle}
	class="shadow"
	placeholder="Song name"
	type="text"
	name="song-name"
	id=""
/>
<button
	on:click={() => searchSong(songTitle)}
	class="bg-blue-500 hover:bg-blue-700 text-white rounded"
	type="button">Search Song</button
>

{#if songsJson && songsJson.songs.length < 1}
	<p>No songs found!</p>
{:else if songsJson}
	{#each songsJson.songs as song}
		<p>{song.title}</p>
	{/each}
{:else}
	<p>Search for a song!</p>
{/if}
