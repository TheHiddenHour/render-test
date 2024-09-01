<script lang="ts">
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

<div class="grid m-4 h-screen">
	<div class="grid gap-4 content-center justify-items-start items-center">
		<p class="text-white text-9xl">ThemeRater</p>
		<p class="text-white text-2xl">Anime OP ratings</p>
		<button class="rounded px-4 py-2 text-white hover:bg-ultra-violet bg-african-violet">Get Started</button>
	</div>
	<div class="grid col-start-2 justify-center items-center">
		<img class="" src="menhera.png" alt="" srcset="" />
	</div>
</div>
