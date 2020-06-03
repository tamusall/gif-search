<script>	
	let searchInput = '';
	let loading = false;
	const API_URL = 'https://api.giphy.com/v1/gifs/search?api_key=LZs2r32x7jSgMEgVaitu42PL64LrWs9D&q=';

	let gifs = [];

	async function formSubmitted(event) {
		event.preventDefault();
		gifs = [];
		loading = true;
		const url = `${API_URL}${searchInput}`;
		const response = await fetch(url);
		const json = await response.json();
		gifs = json.data.map(gif => gif.images.fixed_height.url);
		loading = false;
	}
</script>

<style>
	.results {
		column-count: 3;
	}

	img {
		width: 100%;
		height: auto;
	}

	h1 {
		color: purple;
		justify-content: center;
	}
	h2 {
		color: aquamarine;
		justify-content: center;
	}
</style>

<h1>Ye Olde Gif Engine</h1>
<h2>Powered by Giphy!</h2>

<form id="searchForm" on:submit={formSubmitted}>
	<input bind:value={searchInput} id="search" name="search" />
	<button id="button" type="sumbit">Search</button>
</form>

{#if loading}
<img alt="loading" src="https://media2.giphy.com/media/l3nWhI38IWDofyDrW/giphy.gif?cid=790b76115d055ab7424f75514dcb4d7a&rid=giphy.gif" />
{/if}

<div class="results">
	{#each gifs as gif}
		<img alt="gif" src={gif}>
	{/each}
</div>
