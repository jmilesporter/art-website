<script context="module">
	export async function load({ fetch }) {
		const res = await fetch('https://jsonplaceholder.typicode.com/photos');
		const guides = await res.json();

		if (res.ok) {
			return {
				props: {
					guides
				}
			};
		} else {
			return {
				status: res.status(),
				error: new Error('Could not fetch the guides')
			};
		}
	}
</script>

<script>
	export let guides;
</script>

<div class="guides">
	<ul>
		{#each guides as guide}
			<li>
				<a sveltekit:prefetch href={`/guides/${guide.id}`}>{guide.title}</a>
			</li>
		{/each}
	</ul>
	<div class="links">
		<a href="/guides">Guides</a>
		<a href="/about">About</a>
		<a href="/">Home</a>
	</div>
</div>

<style>
	.guides {
		margin-top: 20px;
	}
	ul {
		list-style-type: none;
		padding: 0;
	}
	a {
		display: inline-block;
		margin-top: 10px;
		padding: 10px;
		border: 1px dotted rgba(255, 255, 255, 0.2);
	}
	.links {
		text-align: center;
		display: block;
		margin: 20px auto;
	}
</style>
