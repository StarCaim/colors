<script lang="ts">
	import ColorBlock from '$lib/components/ColorBlock.svelte';

	const generateColor = () => {
		return Math.random().toString(16).substring(2, 8);
	};

	let pallette: { color: string; locked: boolean }[] = [
		{ color: generateColor(), locked: false },
		{ color: generateColor(), locked: false },
		{ color: generateColor(), locked: false },
		{ color: generateColor(), locked: false },
		{ color: generateColor(), locked: false }
	];

	const onKeyUp = (e: KeyboardEvent) => {
		if (e.key === ' ' || e.key === 'Space') {
			handleGenerateColor();
		}
	};

	const handleGenerateColor = () => {
		pallette = pallette.map((color) => {
			if (!color.locked) {
				color.color = generateColor();
			}
			return color;
		});
	};
</script>

<div class="flex-1 flex flex-col lg:flex-row items-center justify-center">
	{#each pallette as { color }}
		<ColorBlock {color} />
	{/each}
</div>

<svelte:window on:keyup={onKeyUp} />
