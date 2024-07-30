<script lang="ts">
	export let color: string;
	$: color;

	const textColorCheck = (hex: string) => {
		const threshold = 130;

		let r = parseInt(hex.substring(0, 2), 16);
		let g = parseInt(hex.substring(2, 4), 16);
		let b = parseInt(hex.substring(4, 6), 16);

		return r * 0.299 + g * 0.587 + b * 0.114 > threshold ? 'text-black' : 'text-white';
	};

	$: textColor = textColorCheck(color);
</script>

<div
	style="background-color: #{color}"
	class="w-full h-full flex flex-col justify-center lg:justify-end items-start lg:items-center px-16 lg:px-0 py-0 lg:py-24"
>
	<div class="uppercase text-4xl font-semibold {textColor}">
		{color}
	</div>
</div>
