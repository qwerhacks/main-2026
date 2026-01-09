<script lang="ts">
	export let setTab: (tab: 'application' | 'about' | 'info' | 'sponsors' | 'rsvp') => void;
</script>

<div class="space-y-20 py-16 px-4">

	<!-- SECTION 1: HERO STATEMENT -->
	<section class="max-w-5xl mx-auto text-center">
		<div class="glass-card p-10">
			<h1
				class="text-4xl md:text-6xl mb-6"
				style="
					font-family: 'Ranille Normal', serif;
					color: #C5A059;
					text-shadow: 0 0 12px rgba(197, 160, 89, 0.45);
				"
			>
				We’re Not Like Other Hackathons
			</h1>

			<p
				class="text-lg md:text-xl max-w-3xl mx-auto"
				style="font-family: 'Spectral', serif;"
			>
				QWER Hacks is designed to be a space where people can explore, grow, and create — while being supported in expressing their identities and experiences.
			</p>

			<p
				class="text-xl mt-4 italic"
				style="font-family: 'Spectral', serif;"
			>
				Technology is the medium, community is the point.
			</p>
		</div>
	</section>

	<!-- SECTION 2: STAGGERED VALUES -->
	<section class="max-w-6xl mx-auto grid md:grid-cols-3 gap-8">
		<div class="glass-card p-8 md:translate-y-6">
			<h2 class="card-title">Impact</h2>
			<p class="card-text">
				We care about projects rooted in real experiences and real needs — especially those affecting marginalized communities.
			</p>
		</div>

		<div class="glass-card p-8">
			<h2 class="card-title">Joy</h2>
			<p class="card-text">
				Hackathons don’t have to be stressful to be meaningful. We believe in learning, creating, and celebrating together.
			</p>
		</div>

		<div class="glass-card p-8 md:-translate-y-6">
			<h2 class="card-title">Belonging</h2>
			<p class="card-text">
				Whether you’re deeply technical or just starting out, you deserve to feel welcome, supported, and seen.
			</p>
		</div>
	</section>

	<!-- SECTION 3: WHAT DOES THAT MEAN -->
	<section class="max-w-5xl mx-auto">
		<div class="glass-card p-10">
			<h2
				class="text-3xl md:text-4xl mb-6"
				style="font-family: 'Ranille Normal', serif;"
			>
				So what does that mean for you?
			</h2>

			<div
				class="space-y-4 text-lg"
				style="font-family: 'Spectral', serif;"
			>
				<p>
					At QWER Hacks, we’re less interested in perfection and more interested in intention.
				</p>

				<ul class="list-disc pl-6 space-y-2">
					<li>
						Explore <span class="font-semibold">issues you care about</span>
					</li>
					<li>
						Build projects that <span class="font-semibold">uplift others</span>
					</li>
					<li>
						Meet people who value <span class="font-semibold">authenticity</span> and collaboration
					</li>
				</ul>
			</div>
		</div>
	</section>

	<!-- SECTION 4: CTA -->
	<section class="max-w-4xl mx-auto text-center">
		<div class="glass-card p-12">
			<h2
				class="text-3xl md:text-4xl mb-4"
				style="font-family: 'Ranille Normal', serif;"
			>
				Come Build With Us
			</h2>

			<p
				class="text-lg mb-8 max-w-2xl mx-auto"
				style="font-family: 'Spectral', serif;"
			>
				First hackathon or hundredth — if you’re curious, kind, and ready to learn, there’s a place for you here.
			</p>

			<a
				class="apply-button inline-block px-14 py-4 text-xl rounded-full"
	            on:click={() => setTab('application')}
				style="font-family: 'Spectral', serif;"
			>
				Apply Now
			</a>
		</div>
	</section>

</div>

<style>
	.glass-card {
		background: rgba(0, 0, 0, 0.25);
		backdrop-filter: blur(14px);
		border: 1px solid rgba(255, 255, 255, 0.12);
		border-radius: 1.25rem;
		box-shadow: 0 6px 40px rgba(0, 0, 0, 0.2);
		color: white;
	}

	.card-title {
		font-family: 'Ranille Normal', serif;
		font-size: 1.75rem;
		margin-bottom: 0.5rem;
		color: #C5A059;
	}

	.card-text {
		font-family: 'Spectral', serif;
		font-size: 1.05rem;
	}

	.apply-button {
		background: linear-gradient(
			to right,
			#C5A059,
			#E6C97A,
			#C5A059
		);
		color: black;
		font-weight: 600;
		background-size: 200% 200%;
		transition: all 0.3s ease;
	}

	.apply-button:hover {
		background-position: 100% 50%;
		transform: translateY(-2px);
		box-shadow: 0 6px 20px rgba(197, 160, 89, 0.4);
	}
</style>