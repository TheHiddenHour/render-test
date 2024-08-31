<script lang="ts">
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
			console.log(error.message);
		}
	}

    getData()
</script>

<p class="font-bold">404</p>
<p>Page not found ¯\_(ツ)_/¯</p>
<p>Here's a picture of a cat</p>
<img src={imageUrl} alt="" srcset="">