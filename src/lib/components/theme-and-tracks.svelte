<script lang="ts">
	const theme = {
		title: "Time",
		description: "This year's theme invites you to explore the continuum of time: honoring the past, nurturing the present, and innovating for the future. Through technology, we can preserve stories, strengthen communities, and build toward a more equitable tomorrow."
	};

	const tracks = [
		{
			name: "Preserving the Past",
			icons: "🪶📜",
			color: "yellow",
			gradient: "from-yellow-400 via-yellow-300 to-yellow-500",
			borderColor: "border-yellow-400",
			accentColor: "#FCD34D",
			explanation: "Take a moment to slow down, reflect, and commemorate those who came before us. Preserve the past by honoring the stories of marginalized communities and celebrating cultures to better understand where we are today.",
			motivation: [
				"How do we preserve the stories and cultures of marginalized communities?",
				"What communities are left out from being preserved?",
				"How does the internet and AI distort history",
				"Censorship and erasure of historical events, books",
				"How florida removed pulse nightclub memorial rainbow crosswalk",
				"Banned and challenged books"
			],
			projectIdeas: [
				"Honoring queer and BIPOC history",
				"Preserving cultural histories and traditions",
				"Cultural icons and spaces",
				"Older/analog media, software, and hardware",
				"Reflection and memory in digital spaces",
				"Restoration",
				"Communities and intergenerational knowledge",
				"Protecting endangered languages and stories",
				"Exhibits (e.g., Google Maps redrawing Tongva peoples' lands)"
			]
		},
		{
			name: "Nurturing the Present",
			icons: "🌱🚿",
			color: "green",
			gradient: "from-green-400 via-green-300 to-green-500",
			borderColor: "border-green-400",
			accentColor: "#4ADE80",
			explanation: "The challenges of today call for care and creativity. Nurture the present by reimagining how technology can strengthen our communities, protect our planet, and build a more equitable world.",
			motivation: [
				"Sustainability (protecting our planet)",
				"Equity (reducing bias)",
				"Attacks on DEI, algorithmic bias",
				"Expanding accessibility",
				"Strengthen community",
				"Lack of third spaces/places for community"
			],
			projectIdeas: [
				"Sustainable fashion",
				"Environment",
				"Reducing racial/gender bias",
				"Protecting creative works from AI",
				"Health tech"
			]
		},
		{
			name: "Innovating the Future",
			icons: "🤖🚀",
			color: "blue",
			gradient: "from-blue-400 via-blue-300 to-blue-500",
			borderColor: "border-blue-400",
			accentColor: "#60A5FA",
			explanation: "To boldly go where no one has gone before— bring science fiction to life and venture into the unknown. Embrace curiosity and push the boundaries of technology innovations to uplift underserved communities.",
			motivation: [
				"What are the needs of the future",
				"Supporting the \"future\" → like education, health support",
				"How can we use \"newer\"/\"emerging\" tech in novel and creative ways"
			],
			projectIdeas: [
				"Future education tools",
				"Creative coding",
				"Aerospace/space travel",
				"Speculative design",
				"\"Emerging\" technologies (AR/VR, computer vision, robotics, drones)",
				"Assistive tech",
				"Community resilience, strengthening social support systems and community care",
				"Ethical innovation, how AI and automation can be used responsibly and equitably"
			]
		}
	];
</script>

<div class="space-y-12 py-0 px-4" style="background: transparent !important;">
	<!-- Animated gradient background -->
	<div class="fixed inset-0 -z-10 pointer-events-none">
		<div class="absolute top-0 left-0 w-full h-full bg-gradient-to-br from-yellow-500/10 via-green-500/10 to-blue-500/10 animate-gradient-shift"></div>
		<div class="absolute top-1/4 right-0 w-96 h-96 bg-yellow-400/20 rounded-full blur-3xl animate-pulse-slow"></div>
		<div class="absolute bottom-1/4 left-0 w-96 h-96 bg-green-400/20 rounded-full blur-3xl animate-pulse-slow delay-1000"></div>
		<div class="absolute top-1/2 left-1/2 w-96 h-96 bg-blue-400/20 rounded-full blur-3xl animate-pulse-slow delay-2000"></div>
	</div>

	<!-- THEME SECTION -->
	<section class="max-w-5xl mx-auto relative" aria-labelledby="theme-title">
		<div class="theme-card p-10 md:p-12 relative overflow-hidden">
			<!-- Animated border gradient -->
			<div class="absolute inset-0 rounded-2xl bg-gradient-to-r from-yellow-400 via-green-400 to-blue-400 opacity-20 blur-xl animate-gradient-rotate"></div>
			<div class="absolute inset-[2px] rounded-2xl bg-black/20 backdrop-blur-xl"></div>
			
			<div class="relative z-10">
				<div class="text-center mb-8">
					<h1 id="theme-title" class="theme-title text-4xl md:text-6xl mb-6">
						Theme
					</h1>
				</div>

				<h2 class="theme-main-title text-4xl md:text-5xl mb-6 text-center">
					{theme.title}
				</h2>

				<p class="text-lg md:text-xl mb-8 text-center max-w-3xl mx-auto leading-relaxed text-white/90" style="font-family: 'Spectral', serif;">
					{theme.description}
				</p>
			</div>
		</div>
	</section>

	<!-- TRACKS SECTION -->
	<section class="max-w-6xl mx-auto relative" style="background: transparent;" aria-labelledby="tracks-title">
		<div class="text-center mb-12">
			<h1 id="tracks-title" class="tracks-title text-4xl md:text-6xl mb-4">
				Tracks
			</h1>
			<p class="text-lg md:text-xl max-w-2xl mx-auto text-white/90" style="font-family: 'Spectral', serif;">
				Explore three tracks that span across time, from preserving history to nurturing today's communities to innovating for tomorrow.
			</p>
		</div>

		<div class="grid grid-cols-1 lg:grid-cols-3 gap-8" style="background: transparent;">
			{#each tracks as track, index}
				<div class="track-card track-card-{track.color} p-8 flex flex-col relative group" style="--accent-color: {track.accentColor};">
					<!-- Glowing border effect -->
					<div class="absolute inset-0 rounded-2xl opacity-0 group-hover:opacity-100 transition-opacity duration-500" 
						style="background: linear-gradient(135deg, {track.accentColor}40, {track.accentColor}20); filter: blur(20px);"></div>
					
					<!-- Card content -->
					<div class="relative z-10 flex flex-col h-full">
						<div class="mb-6">
							<div class="flex items-center gap-3 mb-4">
								<span class="text-5xl filter drop-shadow-lg">{track.icons}</span>
								<h2 class="track-card-title text-2xl md:text-3xl mb-0" style="color: {track.accentColor};">
									{track.name}
								</h2>
							</div>

							<p class="card-text mb-6 leading-relaxed text-white/90">
								{track.explanation}
							</p>
						</div>

						<div class="border-t border-white/20 pt-6 mb-6 flex-grow">
							<p class="section-label mb-4" style="color: {track.accentColor};">
								Motivation:
							</p>
							<ul class="space-y-2.5 mb-6">
								{#each track.motivation as item}
									<li class="text-sm flex items-start gap-2.5 text-white">
										<span class="bullet-point mt-1.5 flex-shrink-0" style="color: {track.accentColor};">
											<svg width="6" height="6" viewBox="0 0 6 6" fill="currentColor">
												<circle cx="3" cy="3" r="3"/>
											</svg>
										</span>
										<span style="font-family: 'Spectral', serif;">{item}</span>
									</li>
								{/each}
							</ul>
						</div>

						<div class="border-t border-white/20 pt-6">
							<p class="section-label mb-4" style="color: {track.accentColor};">
								Project Topic Ideas:
							</p>
							<ul class="space-y-2.5">
								{#each track.projectIdeas as idea}
									<li class="text-sm flex items-start gap-2.5 text-white">
										<span class="bullet-point mt-1.5 flex-shrink-0" style="color: {track.accentColor};">
											<svg width="6" height="6" viewBox="0 0 6 6" fill="currentColor">
												<circle cx="3" cy="3" r="3"/>
											</svg>
										</span>
										<span style="font-family: 'Spectral', serif;">{idea}</span>
									</li>
								{/each}
							</ul>
						</div>
					</div>
				</div>
			{/each}
		</div>
	</section>

	<!-- CTA SECTION -->
	<section class="max-w-4xl mx-auto text-center relative" aria-labelledby="cta-title">
		<div class="cta-card p-12 relative overflow-hidden">
			<!-- Animated gradient border -->
			<div class="absolute inset-0 rounded-2xl bg-gradient-to-r from-yellow-400 via-green-400 to-blue-400 opacity-30 blur-xl animate-gradient-rotate"></div>
			<div class="absolute inset-[2px] rounded-2xl bg-black/20 backdrop-blur-xl"></div>
			
			<div class="relative z-10">
				<h2 id="cta-title" class="cta-title text-3xl md:text-4xl mb-4">
					Ready to Build Across Time?
				</h2>

				<p class="text-lg mb-8 max-w-2xl mx-auto leading-relaxed text-white/90" style="font-family: 'Spectral', serif;">
					Whether you're preserving the past, nurturing the present, or innovating for the future (or creating something that spans across all three) we can't wait to see what you build!
				</p>

				<p class="text-lg italic cta-accent" style="font-family: 'Spectral', serif;">
					Remember: tracks are suggestions, not requirements. Build what inspires you!
				</p>
			</div>
		</div>
	</section>
</div>

<style>
	/* Theme Section */
	.theme-card {
		position: relative;
		border-radius: 1.25rem;
		box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
	}

	.theme-title {
		font-family: 'Ranille Normal', serif;
		background: linear-gradient(135deg, #FCD34D, #4ADE80, #60A5FA);
		background-size: 200% 200%;
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		background-clip: text;
		animation: gradient-shift 3s ease infinite;
		filter: drop-shadow(0 0 20px rgba(252, 211, 77, 0.5));
	}

	.theme-main-title {
		font-family: 'Ranille Normal', serif;
		background: linear-gradient(135deg, #FCD34D, #4ADE80, #60A5FA);
		background-size: 200% 200%;
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		background-clip: text;
		animation: gradient-shift 3s ease infinite;
		filter: drop-shadow(0 0 15px rgba(96, 165, 250, 0.4));
	}

	/* Tracks Section */
	section {
		background: transparent !important;
	}

	/* Ensure main container has no visible background */
	div[class*="space-y-20"] {
		background: transparent !important;
		border: none !important;
		box-shadow: none !important;
		outline: none !important;
	}

	/* Ensure no background on any wrapper */
	:global(div.w-full.px-4) {
		background: transparent !important;
	}

	.tracks-title {
		font-family: 'Ranille Normal', serif;
		background: linear-gradient(135deg, #FCD34D, #4ADE80, #60A5FA);
		background-size: 200% 200%;
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		background-clip: text;
		animation: gradient-shift 3s ease infinite;
		filter: drop-shadow(0 0 20px rgba(74, 222, 128, 0.5));
	}

	.track-card {
		background: rgba(0, 0, 0, 0.3);
		backdrop-filter: blur(16px);
		border: none;
		border-radius: 1.25rem;
		box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
		transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
		position: relative;
		overflow: hidden;
	}

	.track-card::before {
		content: '';
		position: absolute;
		inset: 0;
		border-radius: 1.25rem;
		padding: 2px;
		background: linear-gradient(135deg, var(--accent-color), transparent);
		-webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
		-webkit-mask-composite: xor;
		mask-composite: exclude;
		opacity: 0;
		transition: opacity 0.4s;
	}

	.track-card:hover {
		transform: translateY(-8px) scale(1.02);
		box-shadow: 0 12px 48px rgba(0, 0, 0, 0.4), 0 0 30px var(--accent-color)40;
	}

	.track-card:hover::before {
		opacity: 1;
	}

	.track-card-title {
		font-family: 'Ranille Normal', serif;
		font-size: 1.75rem;
		margin-bottom: 0.5rem;
		text-shadow: 0 0 20px currentColor;
		transition: all 0.3s;
	}

	.track-card:hover .track-card-title {
		text-shadow: 0 0 30px currentColor, 0 0 40px currentColor;
	}

	.card-text {
		font-family: 'Spectral', serif;
		font-size: 1.05rem;
		line-height: 1.7;
	}

	.section-label {
		font-family: 'Spectral', serif;
		font-size: 0.875rem;
		font-weight: 600;
		text-transform: uppercase;
		letter-spacing: 0.1em;
		text-shadow: 0 0 10px currentColor;
	}

	.bullet-point {
		transition: transform 0.2s;
	}

	.track-card:hover .bullet-point {
		transform: scale(1.3);
	}

	/* CTA Section */
	.cta-card {
		position: relative;
		border-radius: 1.25rem;
		box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
	}

	.cta-title {
		font-family: 'Ranille Normal', serif;
		background: linear-gradient(135deg, #FCD34D, #4ADE80, #60A5FA);
		background-size: 200% 200%;
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		background-clip: text;
		animation: gradient-shift 3s ease infinite;
		filter: drop-shadow(0 0 15px rgba(252, 211, 77, 0.4));
	}

	.cta-accent {
		background: linear-gradient(135deg, #FCD34D, #4ADE80, #60A5FA);
		background-size: 200% 200%;
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		background-clip: text;
		animation: gradient-shift 3s ease infinite;
	}

	/* Animations */
	@keyframes gradient-shift {
		0%, 100% {
			background-position: 0% 50%;
		}
		50% {
			background-position: 100% 50%;
		}
	}

	@keyframes gradient-rotate {
		0% {
			transform: rotate(0deg);
		}
		100% {
			transform: rotate(360deg);
		}
	}

	@keyframes pulse-slow {
		0%, 100% {
			opacity: 0.3;
			transform: scale(1);
		}
		50% {
			opacity: 0.5;
			transform: scale(1.1);
		}
	}

	.animate-gradient-shift {
		animation: gradient-shift 8s ease infinite;
	}

	.animate-gradient-rotate {
		animation: gradient-rotate 20s linear infinite;
	}

	.animate-pulse-slow {
		animation: pulse-slow 4s ease-in-out infinite;
	}

	.delay-1000 {
		animation-delay: 1s;
	}

	.delay-2000 {
		animation-delay: 2s;
	}
</style>