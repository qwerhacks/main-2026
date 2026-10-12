<script lang="ts">
	import Background from '$lib/components/background.svelte';
	import Hero from '$lib/components/hero.svelte';
	import Tracks from '$lib/components/tracks.svelte';
</script>

<div class="w-full h-full overflow-x-hidden overflow-y-auto overscroll-contain">
	<a id="mlh-trust-badge" style="display:block;max-width:100px;min-width:60px;position:fixed;right:50px;top:0;width:10%;z-index:10000" href="https://mlh.io/na?utm_source=na-hackathon&utm_medium=TrustBadge&utm_campaign=2026-season&utm_content=yellow" target="_blank"><img src="https://logged-assets.s3.amazonaws.com/trust-badge/2027/mlh-trust-badge-2027-yellow.svg" alt="Major
  	League Hacking 2027 Hackathon Season" style="width:100%"></a>
	<div id="background" class="absolute w-full h-full -z-10">
		<Background />
	</div>
	<div id="content" class="z-10 flex flex-col items-center justify-center w-screen min-h-screen py-16">
		<Hero />
	</div>
	<div id="content" class="z-10 flex flex-col items-center justify-center w-screen min-h-screen">
		<Tracks />
	</div>
</div>

<style>
.c {
	mix-blend-mode: screen;
}
</style>

<svelte:head>
	<link rel="preload" href="/fonts/NightyDEMO.woff2" as="font" type="font/woff2" crossorigin>
	<link rel="preload" href="/fonts/RanilleNormal-Regular.woff2" as="font" type="font/woff2" crossorigin>
	<link rel="preload" href="/fonts/Reactor7.woff2" as="font" type="font/woff2" crossorigin>
</svelte:head>