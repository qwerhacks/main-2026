<script lang="ts">
	import NikitaImg from './assets/Nikita.jpg';
	import AruushiKaurImg from './assets/AruushiKaur.jpeg';
	import LoreleiTangImg from './assets/LoreleiTang.jpg';
	import AnokhiLuthraImg from './assets/AnokhiLuthra.jpg';
	import SarahZhaoImg from './assets/SarahZhao.jpg';
	import AllisonChengImg from './assets/AllisonCheng.jpg';
	import ChelseaChenImg from './assets/ChelseaChen.jpg';
	import PriyankaSanthoshImg from './assets/Priyanka Santhosh.jpg';
	import JasmineWongphatarakulImg from './assets/JasmineWongphatarakul.JPG';
	import KatieWangImg from './assets/KatieWang.jpg';
	import SophieBarrowmanImg from './assets/Sophie Barrowman.jpg';
	import KatieChungImg from './assets/KatieChung.JPG';
	import MaxCabilanganImg from './assets/MaxCabilangan.JPG';
	import DogImg from './assets/dog.png';
</script>

<section class="about-container p-8 max-w-4xl mx-auto text-white" aria-labelledby="about-title">
	<h1 id="about-title" class="text-4xl md:text-6xl mb-6 text-center" style="font-family: 'Ranille Normal', serif; color: #C5A059; text-shadow: 0 0 10px rgba(197, 160, 89, 0.5);">
		Who We Are
	</h1>
	
	<p class="text-lg md:text-xl mb-8 text-center" style="font-family: 'Spectral', serif;">
		We are UCLA’s first LGBTQIA+ hackathon, founded in 2020!
	</p>

	<h2 class="text-3xl md:text-4xl mb-4 mt-12" style="font-family: 'Ranille Normal', serif;">
		Our Mission
	</h2>
	
	<p class="text-lg mb-4" style="font-family: 'Spectral', serif;">
		QWER Hacks aims to celebrate and increase the visibility of the LGBTQIA+ community in tech by developing products to benefit marginalized individuals and bringing together LGBTQIA+ individuals and allies in a welcoming & fun atmosphere that celebrates identity, intersectionality, and community.
	</p>
	
	<p class="text-lg mb-8" style="font-family: 'Spectral', serif;">
		QWER Hacks aims to mobilize and bring together LGBTQIA+ individuals and allies to uplift marginalized communities, while celebrating authenticity, promoting inclusivity, and enabling shared prosperity.
	</p>

	<h2 class="text-3xl md:text-4xl mb-4 mt-12" style="font-family: 'Ranille Normal', serif;">
		Do social impact and tech go hand in hand?
	</h2>
	
	<p class="text-lg mb-4" style="font-family: 'Spectral', serif;">
		In some cases, yes — yet we must realize that tech is just a tool. Tech is not the end but merely the means to the end.
	</p>
	
	<p class="text-lg mb-4" style="font-family: 'Spectral', serif;">
		In some instances, technology has played an essential role in bringing together members of the community as well as pushing for actionable change. While technology is far from the only way to fight for equity, it is one of the most effective means of mobilization now. We must mobilize people (that includes hackers like you!) because societal progress is by, for, and driven by the people.
	</p>
	
	<p class="text-lg mb-8" style="font-family: 'Spectral', serif;">
		We would love to have you join QWER Hacks 2026 in-person. Come build social impact projects and uplift our queer communities and beyond.
	</p>

	<h2 class="text-3xl md:text-4xl mb-4 mt-12" style="font-family: 'Ranille Normal', serif;">
		Meet the Team
	</h2>
	
	<div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-4 sm:gap-2 md:gap-8 mb-12">
		<!-- External Director -->
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 0ms;">
			<img alt="Nikita Senthil" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={NikitaImg}>
			<div class="font-no text-white text-center">Nikita Senthil</div>
			<div class="text-xs text-gray-400 text-center mt-1">External Director</div>
		</a>
		<!-- Internal Director -->
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 40ms;">
			<img alt="Aruushi Kaur" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={AruushiKaurImg}>
			<div class="font-no text-white text-center">Aruushi Kaur</div>
			<div class="text-xs text-gray-400 text-center mt-1">Internal Director</div>
		</a>
		<!-- Dev Team -->
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 80ms;">
			<img alt="Jerome Teo" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={DogImg}>
			<div class="font-no text-white text-center">Jerome Teo</div>
			<div class="text-xs text-gray-400 text-center mt-1">Dev</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 120ms;">
			<img alt="Alicia Yu" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={DogImg}>
			<div class="font-no text-white text-center">Alicia Yu</div>
			<div class="text-xs text-gray-400 text-center mt-1">Dev</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 160ms;">
			<img alt="Maxine Wu" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={DogImg}>
			<div class="font-no text-white text-center">Maxine Wu</div>
			<div class="text-xs text-gray-400 text-center mt-1">Dev</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 200ms;">
			<img alt="Lorelei Tang" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={LoreleiTangImg}>
			<div class="font-no text-white text-center">Lorelei Tang</div>
			<div class="text-xs text-gray-400 text-center mt-1">Dev</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 240ms;">
			<img alt="Anokhi Luthra" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={AnokhiLuthraImg}>
			<div class="font-no text-white text-center">Anokhi Luthra</div>
			<div class="text-xs text-gray-400 text-center mt-1">Dev</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 280ms;">
			<img alt="Sarah Zhao" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={SarahZhaoImg}>
			<div class="font-no text-white text-center">Sarah Zhao</div>
			<div class="text-xs text-gray-400 text-center mt-1">Dev</div>
		</a>
		<!-- Publicity Team -->
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 0ms;">
			<img alt="Shannon Chau" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={DogImg}>
			<div class="font-no text-white text-center">Shannon Chau</div>
			<div class="text-xs text-gray-400 text-center mt-1">Publicity and Design Chair</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 40ms;">
			<img alt="Melanie Li" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={DogImg}>
			<div class="font-no text-white text-center">Melanie Li</div>
			<div class="text-xs text-gray-400 text-center mt-1">Publicity and Design</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 80ms;">
			<img alt="Cait Nguyen" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={DogImg}>
			<div class="font-no text-white text-center">Cait Nguyen</div>
			<div class="text-xs text-gray-400 text-center mt-1">Publicity</div>
		</a>
		<!-- Spinance Team -->
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 120ms;">
			<img alt="Amy Zhao" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={DogImg}>
			<div class="font-no text-white text-center">Amy Zhao</div>
			<div class="text-xs text-gray-400 text-center mt-1">Spinance</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 160ms;">
			<img alt="Selina Song" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={DogImg}>
			<div class="font-no text-white text-center">Selina Song</div>
			<div class="text-xs text-gray-400 text-center mt-1">Spinance</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 200ms;">
			<img alt="Hannah Park" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={DogImg}>
			<div class="font-no text-white text-center">Hannah Park</div>
			<div class="text-xs text-gray-400 text-center mt-1">Spinance</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 240ms;">
			<img alt="Alexis Raquino" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={DogImg}>
			<div class="font-no text-white text-center">Alexis Raquino</div>
			<div class="text-xs text-gray-400 text-center mt-1">Spinance</div>
		</a>
		<!-- Collab Relations Team -->
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 280ms;">
			<img alt="Allison Cheng" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={AllisonChengImg}>
			<div class="font-no text-white text-center">Allison Cheng</div>
			<div class="text-xs text-gray-400 text-center mt-1">Collab Relations</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 0ms;">
			<img alt="Deepika Sharma" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={DogImg}>
			<div class="font-no text-white text-center">Deepika Sharma</div>
			<div class="text-xs text-gray-400 text-center mt-1">Collab Relations</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 40ms;">
			<img alt="Chelsea Chen" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={ChelseaChenImg}>
			<div class="font-no text-white text-center">Chelsea Chen</div>
			<div class="text-xs text-gray-400 text-center mt-1">Collab Relations</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 80ms;">
			<img alt="Priyanka Santhosh" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={PriyankaSanthoshImg}>
			<div class="font-no text-white text-center">Priyanka Santhosh</div>
			<div class="text-xs text-gray-400 text-center mt-1">Collab Relations</div>
		</a>
		<!-- Operations Team -->
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 120ms;">
			<img alt="Jasmine Wongphatarakul" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={JasmineWongphatarakulImg}>
			<div class="font-no text-white text-center">Jasmine Wongphatarakul</div>
			<div class="text-xs text-gray-400 text-center mt-1">Operations</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 160ms;">
			<img alt="Shivani Hukkeri" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={DogImg}>
			<div class="font-no text-white text-center">Shivani Hukkeri</div>
			<div class="text-xs text-gray-400 text-center mt-1">Operations</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 200ms;">
			<img alt="Katie Wang" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={KatieWangImg}>
			<div class="font-no text-white text-center">Katie Wang</div>
			<div class="text-xs text-gray-400 text-center mt-1">Operations</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 240ms;">
			<img alt="Sophie Barrowman" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={SophieBarrowmanImg}>
			<div class="font-no text-white text-center">Sophie Barrowman</div>
			<div class="text-xs text-gray-400 text-center mt-1">Operations</div>
		</a>
		<!-- Student Experience Team -->
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 280ms;">
			<img alt="Katie Chung" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={KatieChungImg}>
			<div class="font-no text-white text-center">Katie Chung</div>
			<div class="text-xs text-gray-400 text-center mt-1">Student Experience</div>
		</a>
		<a href="#" target="_blank" rel="noopener noreferrer" class="reveal flex flex-col items-center p-4 shadow-md transition-all duration-200 rounded-lg hover:bg-zinc-800/20 focus:bg-zinc-800/50 cursor-pointer revealed" style="transition-delay: 0ms;">
			<img alt="Max Cabilangan" class="rounded-full sm:w-[20vw] sm:h-[20vw] md:w-[15vw] md:h-[15vw] mb-3 object-cover" loading="lazy" src={MaxCabilanganImg}>
			<div class="font-no text-white text-center">Max Cabilangan</div>
			<div class="text-xs text-gray-400 text-center mt-1">Student Experience</div>
		</a>
	</div>

	
	<p class="text-xl font-bold text-center mt-12" style="font-family: 'Spectral', serif;">
		<strong>We’re here, we’re QWER, and can’t wait to see you!</strong>
	</p>
</section>

<style>
	.about-container {
		background: rgba(0, 0, 0, 0.2);
		backdrop-filter: blur(12px);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 1rem;
		box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
	}
</style>
