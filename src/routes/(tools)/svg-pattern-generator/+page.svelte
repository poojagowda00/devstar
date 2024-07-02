<script>
	import { writable } from 'svelte/store';

	const patternTypes = ['Circle', 'Square', 'Triangle', 'Hexagon', 'Right triangle', 'Half circle', 'Dots'];

	let selectedPatternType = patternTypes[0];
	let patternColor = '#47d3ff';
	let backgroundColor = '#474bff';

	let size = 32;
	let spacing = 30;
	let rotation = 0;
	let skew = 0;
	let opacity = 1;

	const resetSettings = () => {
		size = 32;
		spacing = 30;
		rotation = 0;
		skew = 0;
		opacity = 1;
	};
</script>

<div class="card gap-16 items-center mx-auto max-w-screen-xl lg:grid lg:grid-cols-2 overflow-hidden rounded-lg"></div>

<style>
	.pattern {
		background-color: var(--patternColor);
		opacity: var(--opacity);
		transform: rotate(var(--rotation)deg) skew(var(--skew)deg);
	}

	.Circle {
		border-radius: 50%;
	}

	.Square {
		background-color: var(--patternColor);
		
	}

	.Triangle {
		width: 0;
		height: 0;
		border-left: calc(var(--size) / 2) solid transparent;
		border-right: calc(var(--size) / 2) solid transparent;
		border-bottom: var(--size) solid var(--patternColor);
		background: none;
	}

	.RightTriangle {
		width: 0;
		height: 0;
		border-top: var(--size) solid var(--patternColor);
		border-left: var(--size) solid transparent;
		background: none;
	}

	.HalfCircle {
		border-radius: 50% 50% 0 0;
		width: var(--size);
        height: calc(var(--size) / 2);
        background-color: var(--patternColor);
	}

	.Dots {
	  border-radius: 50%;
    
	}

	h1 {
		color: blue;
	}
</style>

<main class="container mx-auto p-4">
	<h1 class="text-2xl font-bold mb-4 text-center">SVG Pattern Generator</h1>

	<div class="flex flex-col space-y-4">
		<div>
			<label for="patternType" class="font-bold">Pattern Type</label>
			<select id="patternType" bind:value={selectedPatternType} class="w-full mt-1 p-2 border rounded font-bold">
				{#each patternTypes as type}
					<option value={type}>{type}</option>
				{/each}
			</select>
		</div>

		<div class="flex space-x-4">
			<div>
				<label for="patternColor" class="font-bold">Pattern Color</label>
				<input type="color" id="patternColor" bind:value={patternColor} class="w-full mt-1 p-2 border rounded">
				<input type="text" bind:value={patternColor} class="w-full mt-1 p-2 border rounded">
			</div>
			<div>
				<label for="backgroundColor" class="font-bold">Background Color</label>
				<input type="color" id="backgroundColor" bind:value={backgroundColor} class="w-full mt-1 p-2 border rounded">
				<input type="text" bind:value={backgroundColor} class="w-full mt-1 p-2 border rounded">
			</div>
		</div>

		<div class="flex items-center justify-between">
			<h2 class="font-bold">Pattern Settings</h2>
			<button on:click={resetSettings} class="bg-gray-300 text-gray-700 px-4 py-2 rounded hover:bg-gray-400 font-bold">Reset</button>
		</div>

		<div class="flex flex-col space-y-2">
			<div>
				<label for="size" class="font-bold">Size: {size}px</label>
				<input type="range" id="size" min="1" max="100" bind:value={size} class="w-full">
			</div>
			<div>
				<label for="spacing" class="font-bold">Spacing: {spacing}px</label>
				<input type="range" id="spacing" min="1" max="100" bind:value={spacing} class="w-full">
			</div>
			<div>
				<label for="rotation" class="font-bold">Rotation: {rotation}deg</label>
				<input type="range" id="rotation" min="0" max="360" bind:value={rotation} class="w-full">
			</div>
			<div>
				<label for="skew" class="font-bold">Skew: {skew}deg</label>
				<input type="range" id="skew" min="0" max="360" bind:value={skew} class="w-full">
			</div>
			<div>
				<label for="opacity" class="font-bold">Pattern Opacity: {opacity}</label>
				<input type="range" id="opacity" min="0" max="1" step="0.1" bind:value={opacity} class="w-full">
			</div>
		</div>
	</div>

	<div class="pattern-container mt-4" style="background-color: {backgroundColor}; display: grid; grid-template-columns: repeat(auto-fill, minmax({size + spacing}px, 1fr)); gap: {spacing}px;">
		{#each Array(50) as _, i}
		   <div class="pattern {selectedPatternType}" style="
		       width: {size}px;
		       height: {size}px;
		       background-color: {patternColor};
		       opacity: {opacity};
		       transform: rotate({rotation}deg) skew({skew}deg);">
	        </div>		
		{/each}
	</div>
</main>
