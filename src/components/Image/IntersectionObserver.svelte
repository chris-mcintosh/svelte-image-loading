<script>
	import { onMount } from 'svelte';
	export let once = false;
  let intersecting = false;
  
	let container;
	onMount(() => {
		if (typeof IntersectionObserver !== 'undefined') {
			//const rootMargin = `${bottom}px ${left}px ${top}px ${right}px`;
			const rootMargin = `150px`;
			const observer = new IntersectionObserver(entries => {
				intersecting = entries[0].isIntersecting;
				if (intersecting && once) {
					observer.unobserve(container);
				}
			}, {
				rootMargin
			});
			observer.observe(container);
			return () => observer.unobserve(container);
		}
	});
</script>

<style>
	div {
		width: 100%;
		height: 100%;
	}
</style>

<div bind:this={container}>
	<slot {intersecting}></slot>
</div>
