<script context="module">
	export async function load({ fetch, params }) {
		const id = params.id;
		const response = await fetch(`https://jsonplaceholder.typicode.com/photos/${id}`);
		const guide = await response.json();

		if (response.ok) {
			return {
				props: {
					guide
				}
			};
		}
		return {
			status: response.status(),
			error: new Error('Could not load guide')
		};
	}
</script>

<script>
	export let guide;
</script>

<div class="guide">
	<h2>{guide.title}</h2>
	<img src={guide.url} alt="image ${guide.id}" />
</div>

<style>
	.guide {
		margin-top: 40px;
		padding: 10px;
		border: 1px dotted rgba(255, 255, 255, 0.2);
	}
</style>
