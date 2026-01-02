<script lang="ts">
	import Background from '$lib/components/background.svelte';
	import Hero from '$lib/components/hero.svelte';
	import Application from '$lib/components/application.svelte';
	import About from '$lib/components/about.svelte';
	import Sponsors from '$lib/components/sponsors.svelte';
	import Rsvp from '$lib/components/rsvp.svelte';
	import Navbar from '$lib/components/navbar.svelte';

	let activeTab: 'application' | 'about' | 'sponsors' | 'rsvp' = 'rsvp';
</script>

<div class="w-full h-full overflow-y-auto overscroll-contain">
	<a
		id="mlh-trust-badge"
		style="display:block;max-width:100px;min-width:60px;position:fixed;right:5%;top:0;width:10%;z-index:10000"
		href="https://mlh.io/na?utm_source=na-hackathon&utm_medium=TrustBadge&utm_campaign=2026-season&utm_content=gray"
		target="_blank"
		><img
			src="https://s3.amazonaws.com/logged-assets/trust-badge/2026/mlh-trust-badge-2026-gray.svg"
			alt="Major League Hacking 2026 Hackathon Season"
			style="width:100%"
		/></a
	>
	<div id="background" class="fixed w-full h-full -z-10">
		<Background />
	</div>
	<div class="sticky top-0 z-50 w-full">
		<Navbar bind:activeTab />
	</div>
	<div class="w-full max-w-none h-auto pt-10 pb-10 flex flex-col items-center justify-center z-20 relative px-4">
		<h1 class="text-6xl sm:text-6xl md:text-8xl text-white font-serif drop-shadow-[0_5px_5px_rgba(0,0,0,0.3)] transition-transform duration-300 hover:scale-110 cursor-default text-center break-words max-w-full" style="font-family: 'Milonga', serif;">
			✨QWER Hacks✨
		</h1>
		<p class="text-xl sm:text-2xl md:text-3xl text-white mt-2 font-serif drop-shadow-[0_5px_5px_rgba(0,0,0,0.3)] transition-transform duration-300 hover:scale-110 cursor-default text-center" style="font-family: 'Ranille Normal', serif;">
			UCLA | Feb 7-8, 2026
		</p>
		<a 
			href="https://docs.google.com/forms/d/e/1FAIpQLSfWmQDnkrIx32-oQlLF6Y4ucjvX7JUtfnNSwMgA0Xt-7M9mAQ/viewform"
			target="_blank"
			rel="noopener noreferrer"
			class="inline-block mt-6 px-8 py-3 bg-[#C5A059] text-white font-bold text-xl sm:text-2xl uppercase tracking-wider rounded-full shadow-[0_5px_15px_rgba(0,0,0,0.3)] transition-all duration-300 hover:scale-105 hover:bg-[#b08d4d] hover:shadow-[0_8px_20px_rgba(0,0,0,0.4)] cursor-pointer text-center no-underline" 
			style="font-family: 'Ranille Normal', serif;"
		>
			Apply Now
		</a>
	</div>
	<div id="content" class="z-10 flex flex-col items-center justify-center w-full pb-20">
		{#if activeTab === 'application'}
			<Application />
		{:else if activeTab === 'rsvp'}
			<Rsvp />
		{:else if activeTab === 'about'}
			<div class="w-full px-4">
				<About />
			</div>
		{:else if activeTab === 'sponsors'}
			<div class="w-full px-4">
				<Sponsors />
			</div>
		{/if}
	</div>
	<footer class="footer w-full text-center pb-10 z-20 relative">
		<a
			href="https://github.com/MLH/mlh-policies/blob/main/code-of-conduct.md"
			target="_blank"
			rel="noopener noreferrer"
			class="footer-link"
		>
			MLH Code of Conduct
		</a>
		| Made with ˚ʚ♡ɞ˚ by the QWER Hacks organizing team!
	</footer>
</div>

<svelte:head>
	<link rel="preload" href="/fonts/NightyDEMO.woff2" as="font" type="font/woff2" crossorigin />
	<link
		rel="preload"
		href="/fonts/RanilleNormal-Regular.woff2"
		as="font"
		type="font/woff2"
		crossorigin
	/>
	<link rel="preload" href="/fonts/Reactor7.woff2" as="font" type="font/woff2" crossorigin />
	<link rel="preload" href="/fonts/Milonga-Regular.ttf" as="font" type="font/ttf" crossorigin />
</svelte:head>

<style>
	#main-content {
		min-height: 100vh; /* Full viewport height */
	}
	.c {
		mix-blend-mode: screen;
	}
	footer.footer {
		color: #ffffff;
		font-family: 'Spectral', serif;
		font-size: 0.9rem;
	}

	a.footer-link {
		color: #ffffff;
		text-decoration: underline;
	}

	a.footer-link:hover {
		color: #fef08a;
	}
	
</style>
