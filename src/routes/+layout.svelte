<script lang="ts">
	import '../app.css';
	import { themes } from '$lib/themes';
	import { onMount } from 'svelte';

	let currentTheme = '';

	onMount(() => {
		if (typeof window !== 'undefined') {
			const theme = window.localStorage.getItem('theme');
			if (theme && themes.includes(theme)) {
				document.documentElement.setAttribute('data-theme', theme);
				currentTheme = theme;
			} else {
				document.documentElement.setAttribute('data-theme', 'system');
				currentTheme = 'system';
			}
		}
	});

	const setTheme = (event: Event) => {
		const select = event.target as HTMLSelectElement;
		const theme = select.value;

		if (themes.includes(theme)) {
			const oneYear = 60 * 60 * 24 * 365;
			window.localStorage.setItem('theme', theme);
			document.cookie = `theme=${theme}; max-age=${oneYear}; path=/`;
			document.documentElement.setAttribute('data-theme', theme);
			currentTheme = theme;
		}
	};
</script>

<div class="min-h-dvh h-dvh flex flex-col overflow-hidden p-4">
	<div class="flex justify-end">
		<select
			data-choose-theme
			class="select select-bordered select-md capitalize w-full max-w-32 bg-base-200"
			on:change={setTheme}
			bind:value={currentTheme}
		>
			{#each themes as theme}
				<option value={theme} class="capitalize">{theme}</option>
			{/each}
		</select>
	</div>
	<slot />
</div>
