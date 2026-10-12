<script lang="ts">
	import Email from './email.svelte';
</script>

<div class="mt-auto" />

<div
	class="hero-card flex flex-col justify-center items-center gap-8 p-10 md:p-14 rounded-3xl w-max lg:w-[60%] max-w-[95vw] md:max-w-[70vw]"
>
	<!-- Logo from 2023 commented out for now; replaced with plain heading text -->
	<div
		class="text-center font-milonga tracking-wide flex flex-col items-center gap-5 md:gap-6"
	>
		<span class="text-6xl md:text-7xl lg:text-8xl text-white qwer-title" style="text-shadow: 0 10px 30px rgba(0,0,0,0.45), 0 3px 8px rgba(34,34,34,0.2);"> ݁₊⊹.QWER Hacks.₊⊹</span>
		<span class="text-3xl md:text-4xl lg:text-5xl" style="color: #1a1560; opacity: 0.9;">UCLA&nbsp;·&nbsp;Jan 16–17, 2027</span>
	</div>

	<div class="flex flex-col items-center gap-4">
		<a
			href="https://forms.gle/okVWdD28y26edwbP9"
			target="_blank"
			rel="noopener noreferrer"
			class="px-8 py-4 text-xl lg:text-2xl font-montserrat_alternates_bold text-white transition-all duration-300 hover:scale-105"
			style="
				background:#D4AF37;
				border-radius:999px;
				box-shadow: 0 8px 20px rgba(0,0,0,0.3), 0 2px 6px rgba(0,0,0,0.2);
			"
		>
			Fill Out Our Early Interest Form →
		</a>

		<p
			class="text-center text-lg lg:text-xl font-montserrat_alternates"
			style="color: #1a1560; opacity: 0.9;"
		>
			Get updates about QWER Hacks 2027, applications, and announcements.
		</p>
	</div>

	<span
		class="text-center text-2xl lg:text-3xl font-montserrat_alternates_bold inline-block leading-relaxed"
		style="color: #1a1560; opacity: 0.9;"
		>the lgbtqia community? <wbr />at MY hackathon???<br /><br />it's more likely than you think.</span
	>
	<a
		href="http://mlh.io/code-of-conduct"
		class="underline underline-offset-4 font-montserrat_alternates_bold text-xl text-[#1a1560] opacity-80 transition-opacity duration-300 hover:opacity-100"
		>MLH Code of Conduct</a
	>
</div>

<!--2024's sponsorship form-->
<div
	class="mt-auto max-w-prose text-center py-5 px-5 text-white font-montserrat_alternates text-2xl lg:text-3xl"
>
	<!--Interested in helping us make this event happen? <a href="https://drive.google.com/file/d/1bEVtQlb4Yw58R0a8gH0P0BWTpXJEpXQC/view" class="underline text-sky-light">Check out our sponsorship packet</a>!>-->
</div>

<style>
	.hero-card {
		background: rgba(255, 255, 255, 0.12);
		backdrop-filter: blur(14px) saturate(120%);
		-webkit-backdrop-filter: blur(14px) saturate(120%);
		border: 1px solid rgba(255, 255, 255, 0.25);
		box-shadow: 0 20px 60px rgba(10, 55, 161, 0.25), 0 4px 12px rgba(0, 0, 0, 0.15);
	}

	.qwer-title {
		cursor: pointer;
		position: relative;
		transition: transform 0.3s ease, text-shadow 0.3s ease;
	}

	.qwer-title:hover {
		transform: scale(1.05);
		text-shadow: 0 10px 40px rgba(255,255,255,0.6), 0 3px 8px rgba(255,255,255,0.4);
		animation: sparkle-glow 1.5s ease-in-out infinite;
	}

	@keyframes sparkle-glow {
		0%, 100% {
			filter: brightness(1) drop-shadow(0 0 5px rgba(255,255,255,0.3));
		}
		25% {
			filter: brightness(1.15) drop-shadow(0 0 15px rgba(255,255,255,0.6));
		}
		50% {
			filter: brightness(1.1) drop-shadow(0 0 20px rgba(255,255,255,0.5));
		}
		75% {
			filter: brightness(1.15) drop-shadow(0 0 15px rgba(255,255,255,0.6));
		}
	}
</style>
