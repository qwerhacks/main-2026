<script lang="ts">
	import { onMount } from 'svelte';

	let stars: { top: number; left: number; size: number; delay: number; duration: number; type: 'five-point' | 'sparkle' | 'emoji-sparkle' }[] = [];

	onMount(() => {
		stars = Array.from({ length: 70 }).map(() => {
			const typeRandom = Math.random();
			let type: 'five-point' | 'sparkle' | 'emoji-sparkle';
			
			if (typeRandom > 0.3) {
				type = 'sparkle';
			} else if (typeRandom > 0.1) {
				type = 'five-point';
			} else {
				type = 'emoji-sparkle';
			}

			let size = Math.random() * (Math.random() > 0.8 ? 10 : 8) + 2;
			// Make emojis slightly larger so they are visible
			if (type === 'emoji-sparkle') {
				size = Math.random() * 15 + 10;
			}

			return {
				top: Math.random() * 100,
				left: Math.random() * 100,
				size: size,
				delay: Math.random() * 5,
				duration: Math.random() * 5 + 3,
				type: type
			};
		});
	});
</script>

<div class="w-full h-full relative overflow-hidden" style="background: linear-gradient(90deg, #143072 0%, #b8e9c0 100%);">
	{#each stars as star}
		<div
			class="star {star.type}"
			style="top: {star.top}%; left: {star.left}%; width: {star.size}px; height: {star.size}px; animation-delay: {star.delay}s; animation-duration: {star.duration}s; font-size: {star.size}px; line-height: 1;"
		>
			{#if star.type === 'emoji-sparkle'}
				✨
			{/if}
		</div>
	{/each}
</div>

<style>
	.star {
		position: absolute;
		background: white;
		opacity: 0.9;
		filter: drop-shadow(0 0 4px rgba(255, 255, 255, 1)) drop-shadow(0 0 8px rgba(255, 255, 255, 0.8));
	}

	.five-point {
		clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
		animation: float-sparkle infinite ease-in-out alternate;
	}

	.sparkle {
		clip-path: polygon(50% 0%, 60% 40%, 100% 50%, 60% 60%, 50% 100%, 40% 60%, 0% 50%, 40% 40%);
		animation: float-sparkle infinite ease-in-out alternate;
	}

	.emoji-sparkle {
		background: transparent;
		display: flex;
		align-items: center;
		justify-content: center;
		animation: float-sparkle infinite ease-in-out alternate;
	}

	@keyframes float-sparkle {
		0% { transform: translate(0, 0) rotate(0deg); }
		100% { transform: translate(10px, -20px) rotate(15deg); }
	}
</style>
