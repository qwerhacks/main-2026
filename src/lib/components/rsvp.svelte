<script lang="ts">
	import { onMount } from 'svelte';

	let isLoaded = false;

	onMount(() => {
		setTimeout(() => {
			isLoaded = true;
		}, 300);
	});

	let loading = false;
	let success = false;
	let error = '';

	let email = '';
	let fullName = '';
	let attending = '';
	let dietary = '';
	let accommodations = '';
	let photoRelease = false;
	let swag = '';
	let tShirtSize = '';
	let lanyardColor = '';
	let questions = '';
	let excitement = '';

	const attendingOptions = ['yes !!', 'no :(', 'maybe !?'];
	const accommodationOptions = ['Yes', 'Maybe', 'No'];
	const swagOptions = ['Yes', 'No'];
	const sizeOptions = ['S', 'M', 'L', 'XL'];
	const lanyardOptions = ['Option 1'];
	const excitementOptions = [
		'incredibly, unbelievably excited! beyond ecstatic',
		'wow wow wow QWER HACKS ??? color me stoked!',
		"jiminy cricket! it's QWER Hacks time????",
		'yes.'
	];

	async function handleSubmit() {
		loading = true;
		error = '';
		
		const GOOGLE_FORM_URL = 'https://docs.google.com/forms/d/e/1FAIpQLSduAIUTyK0EMo4nQVEvlUAJt1DohMtpXqtXQsYchILpZ503Yg/formResponse';
		
		const params = new URLSearchParams();
		params.append('emailAddress', email);
		params.append('entry.1121294892', fullName);
		params.append('entry.2054358389', attending);
		params.append('entry.1915173830', dietary);
		params.append('entry.2123894270', accommodations);
		if (photoRelease) {
			params.append('entry.981008060', 'I grant permission to UCLA, SWE, MLH, Daily Bruin, and QWER Hacks');
		}
		params.append('entry.789968030', swag);
		if (swag === 'Yes') {
			params.append('entry.1851495409', tShirtSize);
			params.append('entry.161316649', lanyardColor);
		}
		params.append('entry.440083840', questions);
		params.append('entry.101038521', excitement);
		
		// Hidden fields required for submission
		params.append('fvv', '1');
		params.append('fbzx', '4349901971409952763');
		params.append('pageHistory', '0,1,2');
		params.append('draftResponse', '[null,null,"4349901971409952763"]');
		params.append('submissionTimestamp', '-1');

		try {
			await fetch(GOOGLE_FORM_URL, {
				method: 'POST',
				mode: 'no-cors',
				credentials: 'include',
				headers: {
					'Content-Type': 'application/x-www-form-urlencoded'
				},
				body: params
			});
			success = true;
		} catch (err) {
			console.error(err);
			error = 'Something went wrong. Please try again.';
		} finally {
			loading = false;
		}
	}
</script>

<div class="container">
	<div class="scroll-paper {isLoaded ? 'slide-in' : 'slide-out'}">
		<div class="scroll-content" aria-label="RSVP form">
			<div class="postcard">
				<div class="right">
					<form on:submit|preventDefault={handleSubmit}>
						{#if !success}
							<div class="input-group flex-col flex">
								<label class="input-label rubik purple"><span style="font-size: 1.5em;">RSVP</span></label>
								<p class="spectral italic text-sm text-gray-500 mb-4">Please fill in your details below.</p>
							</div>

							<!-- Email -->
							<div class="input-group flex-col flex">
								<label class="input-label rubik purple" for="email">Email *</label>
								<input type="email" id="email" bind:value={email} required class="input-field spectral italic w-full" placeholder="your@email.com" />
							</div>

							<!-- Name -->
							<div class="input-group flex-col flex">
								<label class="input-label rubik purple" for="fullName">Full Name *</label>
								<input type="text" id="fullName" bind:value={fullName} required class="input-field spectral italic w-full" placeholder="Jane Doe" />
							</div>

							<!-- Attending -->
							<div class="input-group flex-col flex">
								<label class="input-label rubik purple">Will you be attending QWER Hacks? *</label>
								<div class="flex flex-wrap gap-4 mt-2">
									{#each attendingOptions as option}
										<label class="flex items-center gap-2 cursor-pointer checkbox-label">
											<input type="radio" bind:group={attending} value={option} required class="checkbox-input" />
											<span class="ml-2">{option}</span>
										</label>
									{/each}
								</div>
							</div>

							<!-- Dietary -->
							<div class="input-group flex-col flex">
								<label class="input-label rubik purple" for="dietary">Dietary Restrictions *</label>
								<input type="text" id="dietary" bind:value={dietary} required class="input-field spectral italic w-full" placeholder="Vegetarian, Gluten-free, etc. (or 'None')" />
							</div>

							<!-- Accommodations -->
							<div class="input-group flex-col flex">
								<label class="input-label rubik purple">Do you need overnight accommodations?</label>
								<p class="spectral italic text-sm text-gray-500 mb-2">The venue does not allow sleeping overnight.</p>
								<div class="flex flex-wrap gap-4">
									{#each accommodationOptions as option}
										<label class="flex items-center gap-2 cursor-pointer checkbox-label">
											<input type="radio" bind:group={accommodations} value={option} class="checkbox-input" />
											<span class="ml-2">{option}</span>
										</label>
									{/each}
								</div>
							</div>

							<!-- Photo Release -->
							<div class="checkbox-container">
								<input type="checkbox" bind:checked={photoRelease} id="photoRelease" required class="checkbox-input" />
								<label for="photoRelease" class="checkbox-label ml-2">
									I hereby grant permission to UCLA, SWE, MLH, Daily Bruin, and QWER Hacks to use photographs and/or video of me taken on February 7th and 8th, 2026 at UCLA in publications, news releases, online and in other communications related to the mission of QWER Hacks. *
								</label>
							</div>

							<!-- Swag -->
							<div class="input-group flex-col flex mt-4">
								<label class="input-label rubik purple">Would you like to receive swag from us?</label>
								<div class="flex flex-wrap gap-4 mt-2">
									{#each swagOptions as option}
										<label class="flex items-center gap-2 cursor-pointer checkbox-label">
											<input type="radio" bind:group={swag} value={option} class="checkbox-input" />
											<span class="ml-2">{option}</span>
										</label>
									{/each}
								</div>
							</div>

							{#if swag === 'Yes'}
								<!-- T-Shirt -->
								<div class="input-group flex-col flex pl-4 border-l-2 border-gray-300 mt-2">
									<label class="input-label rubik purple">T-Shirt Size *</label>
									<div class="flex flex-wrap gap-4 mt-2">
										{#each sizeOptions as option}
											<label class="flex items-center gap-2 cursor-pointer checkbox-label">
												<input type="radio" bind:group={tShirtSize} value={option} required class="checkbox-input" />
												<span class="ml-2">{option}</span>
											</label>
										{/each}
									</div>
								</div>

								<!-- Lanyard -->
								<div class="input-group flex-col flex pl-4 border-l-2 border-gray-300 mt-2">
									<label class="input-label rubik purple">Lanyard Color</label>
									<div class="flex flex-wrap gap-4 mt-2">
										{#each lanyardOptions as option}
											<label class="flex items-center gap-2 cursor-pointer checkbox-label">
												<input type="radio" bind:group={lanyardColor} value={option} class="checkbox-input" />
												<span class="ml-2">{option}</span>
											</label>
										{/each}
									</div>
								</div>
							{/if}

							<!-- Questions -->
							<div class="input-group flex-col flex mt-4">
								<label class="input-label rubik purple" for="questions">Questions / Comments</label>
								<textarea id="questions" bind:value={questions} class="input-field spectral italic w-full h-24 p-2" placeholder="Anything else?"></textarea>
							</div>

							<!-- Excitement -->
							<div class="input-group flex-col flex">
								<label class="input-label rubik purple">How excited are you for QWER Hacks?! *</label>
								<div class="flex flex-col gap-2 mt-2">
									{#each excitementOptions as option}
										<label class="flex items-center gap-2 cursor-pointer checkbox-label">
											<input type="radio" bind:group={excitement} value={option} required class="checkbox-input" />
											<span class="ml-2">{option}</span>
										</label>
									{/each}
								</div>
							</div>

							<!-- Submit -->
							<div class="w-full flex justify-center items-center mt-6 mb-6">
								{#if !loading}
									<button type="submit" class="submit-btn rubik-submit">Submit RSVP</button>
								{:else}
									<div class="lds-ripple"><div></div><div></div></div>
								{/if}
							</div>

							{#if error}
								<p class="text-red-500 text-center">{error}</p>
							{/if}
						{:else}
							<div class="text-center py-20">
								<h2 class="rubik purple text-2xl mb-4">You're on the list!</h2>
								<p class="spectral italic text-xl">Thanks for RSVPing. We can't wait to see you!</p>
							</div>
						{/if}
					</form>
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	@import url(https://fonts.googleapis.com/css2?family=Spectral:ital,wght@0,200;0,300;0,400;0,500;0,600;0,700;0,800;1,200;1,300;1,400;1,500;1,600;1,700;1,800&display=swap);
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	.container {
		/* width: 60%; */
		/* max-width: 500px; */
		height: auto;
		aspect-ratio: 500/600;
		/* min-height: auto; */
		perspective: 800px;
	}

	@media (max-width: 400px) {
		/* Target small screens like phones */
		.container {
			width: 90%;
		}
		.overlay-text {
			font-size: 14px;
		}
		.rubik {
			font-size: 12px;
		}
		.input-field {
			font-size: 12px;
		}
		.address {
			font-size: 10px;
		}
		.rubik-submit {
			font-size: 11px;
		}
		.checkbox-label {
			font-size: 11px;
		}
	}
	@media (min-width: 400px) {
		/* Target small screens like phones */
		.container {
			width: 80%;
		}
		.overlay-text {
			font-size: 19px;
		}
		.rubik {
			font-size: 13px;
		}
		.input-field {
			font-size: 13px;
		}
		.address {
			font-size: 11px;
		}
		.rubik-submit {
			font-size: 11px;
		}
		.checkbox-label {
			font-size: 12px;
		}
	}
	@media (min-width: 500px) {
		/* Target small screens like phones */
		.container {
			width: 85%;
		}
		.overlay-text {
			font-size: 24px;
		}
		.rubik {
			font-size: 14px;
		}
		.rubik-submit {
			font-size: 14px;
		}
		.input-field {
			font-size: 14px;
		}
		.checkbox-label {
			font-size: 13px;
		}
		.checkbox-input {
			width: 15px;
			height: 15px;
		}
		.checkbox-input:checked::before {
			font-size: 12px;
		}
	}
	@media (min-width: 585px) {
		.container {
			width: 80%; /* Narrower width */
		}
		.overlay-text {
			font-size: 28px;
		}
		.rubik {
			font-size: 15px;
		}
		.input-field {
			font-size: 15px;
		}
		.address {
			font-size: 13px;
		}
		.checkbox-label {
			font-size: 14px;
		}
		.checkbox-input {
			width: 16px;
			height: 16px;
		}
		.checkbox-input:checked::before {
			font-size: 13px;
		}
	}
	@media (min-width: 768px) {
		.container {
			width: 75%; /* Narrower width */
		}
		.overlay-text {
			font-size: 28px;
		}
		.rubik-submit {
			font-size: 16px;
		}
		.rubik {
			font-size: 16px;
		}
		.input-field {
			font-size: 16px;
		}
		.checkbox-label {
			font-size: 14px;
		}
		.checkbox-input {
			width: 17px;
			height: 17px;
		}
		.checkbox-input:checked::before {
			font-size: 14px;
		}
	}
	/* Extra-large screens (min-width: 1200px) */
	@media (min-width: 900px) {
		.container {
			width: 60%; /* Narrow width for big screens */
		}
		.overlay-text {
			font-size: 29px;
		}
		.rubik-submit {
			font-size: 17px;
		}
		.rubik {
			font-size: 20px;
		}
		.input-field {
			font-size: 20px;
		}
		.checkbox-label {
			font-size: 15px;
		}
		.checkbox-input {
			width: 18px;
			height: 18px;
		}
		.checkbox-input:checked::before {
			font-size: 15px;
		}
	}
	@media (min-width: 1200px) {
		.container {
			width: 60%; /* Narrow width for big screens */
		}
		.overlay-text {
			font-size: 29px;
		}
		.rubik-submit {
			font-size: 19px;
		}
		.rubik {
			font-size: 20px;
		}
		.input-field {
			font-size: 20px;
		}
		.checkbox-label {
			font-size: 17px;
		}
		.checkbox-input {
			width: 19px;
			height: 19px;
		}
		.checkbox-input:checked::before {
			font-size: 16px;
		}
	}
	@media (min-width: 1500px) {
		.container {
			width: 60%; /* Narrow width for big screens */
		}
		.overlay-text {
			font-size: 29px;
		}
		.rubik-submit {
			margin-top: 10px;
			font-size: 21px;
		}
		.rubik {
			font-size: 22px;
		}
		.input-field {
			font-size: 22px;
		}
		.checkbox-label {
			font-size: 18px;
		}
		.checkbox-input {
			width: 20px;
			height: 20px;
		}
		.checkbox-input:checked::before {
			font-size: 17px;
		}
	}
	@media (min-width: 1800px) {
		.container {
			width: 60%; /* Narrow width for big screens */
		}
		.overlay-text {
			font-size: 29px;
		}
		.rubik-submit {
			margin-top: 20px;
			font-size: 24px;
		}
		.rubik {
			font-size: 28px;
		}
		.input-field {
			font-size: 28px;
		}
		.checkbox-label {
			font-size: 20px;
		}
		.checkbox-input {
			width: 22px;
			height: 22px;
		}
		.checkbox-input:checked::before {
			font-size: 19px;
		}
	}
	/* .container {
		width: 90vw;
		height: 
		max-width: 500px;
		max-height: 354px;
		perspective: 800px;
	} */
	@media (min-aspect-ratio: 5/7) and (max-aspect-ratio: 7/5) {
		.container {
			width: 85vw; /* Adjust for squarer screens */
			height: auto;
		}
		.rubik-submit {
			margin-top: 20px;
			font-size: 1.8vw;
		}
		.rubik {
			font-size: 1.9vw;
		}
		.checkbox-label {
			font-size: 1.6vw;
		}
		.input-field {
			font-size: 1.9vw;
		}
		.address {
			font-size: 1.7vw;
		}
	}

	.front {
		position: relative;
		width: 100%;
		padding-bottom: 70.8%;
	}

	.front img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		position: absolute;
	}
	.overlay-text {
		position: absolute;
		top: 6%; /* Adjust to your needs */
		right: 2%; /* Adjust to your needs */
		/* background-color: rgba(0, 0, 0, 0.6); Optional: to make the text stand out */
		color: black;
		padding: 5px 10px;
		/* font-size: 29px; */
		border-radius: 5px;
		rotate: 10deg;
	}
	.slide-in {
		/* Starting state for sliding in */
		top: 100vh; /* Start off-screen */
		animation: slideIn 1s forwards; /* Optional: using keyframes */
	}

	.scroll-paper.slide-out {
		top: 100vh; /* Keep it outside the viewport */
	}

	.scroll-paper {
		height: 100%;
		width: 100%;
		position: relative;
		transition: top 500ms ease;
		top: 100vh;
		background-color: #fdfbf7;
		box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
		margin: 20px 0;
	}

	.scroll-paper::before {
		content: '';
		position: absolute;
		top: -20px;
		left: -5%;
		width: 110%;
		height: 40px;
		background: linear-gradient(to bottom, #d4c5a9 0%, #fdfbf7 50%, #d4c5a9 100%);
		border-radius: 20px;
		box-shadow: 0 5px 10px rgba(0, 0, 0, 0.3);
		z-index: 10;
	}

	.scroll-paper::after {
		content: '';
		position: absolute;
		bottom: -20px;
		left: -5%;
		width: 110%;
		height: 40px;
		background: linear-gradient(to bottom, #d4c5a9 0%, #fdfbf7 50%, #d4c5a9 100%);
		border-radius: 20px;
		box-shadow: 0 5px 10px rgba(0, 0, 0, 0.3);
		z-index: 10;
	}
	@keyframes slideIn {
		from {
			top: 100vh; /* Start off-screen */
		}
		to {
			top: 0; /* Move to the center */
		}
	}

	.scroll-content {
		height: 100%;
		width: 100%;
		padding: 2rem;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		overflow: hidden;
	}

	.email-form {
		position: absolute;
		top: 82%; /* Adjust this value to control vertical position */
		width: 85%; /* Adjust width to fit within the postcard */
		display: flex;
		/* flex-direction: column; */
	}
	input::placeholder,
	.spectral {
		text-align: left;
		font-family: 'Spectral', serif;
		font-weight: 400;
		/* color: #9ca3a3; */
	}
	.italic {
		font-style: italic;
	}

	.right {
		width: 100%;
		height: 100%; /* Ensure both the left and right sides take up equal space */
		overflow-y: auto; /* Enable vertical scrolling */
		max-height: 100%; /* Ensure it doesn't exceed the container height */
		padding-right: 10px; /* Add some padding for the scrollbar */
	}

	/* Add custom scrollbar styling */
	.right::-webkit-scrollbar {
		width: 6px;
	}

	.right::-webkit-scrollbar-track {
		background: #fdfbf7;
		border-radius: 3px;
	}

	.right::-webkit-scrollbar-thumb {
		background: #2c539e;
		border-radius: 3px;
	}

	.right::-webkit-scrollbar-thumb:hover {
		background: #1e3c78;
	}

	/* Ensure form takes full width */
	.right form {
		width: 100%;
	}

	/* Add some spacing between form elements */
	.input-group {
		margin-bottom: 15px;
	}

	/* Adjust the submit button container to stay at bottom */
	.right .w-full.flex-col.flex.justify-center.items-center {
		margin-top: 20px;
		margin-bottom: 20px;
	}

	input,
	button {
		background-color: #fdfbf7;
		outline: solid 0.5px #abb2b2;
	}
	input {
		/* The input will always be 50% of the viewport width */
		padding: 1vw; /* Padding adjusts based on viewport width */
		/* font-size: 0vw; */
	}
	input,
	.welcome {
		border: none; /* Remove all borders */
		border-bottom: 0.5px solid #abb2b2; /* Apply only bottom border */
		padding: 5px; /* Optional: Add padding */
		outline: none;
		/* font-size: 20px; */
	}
	.address {
		border: none; /* Remove all borders */
		border-bottom: 0.5px solid #abb2b2; /* Apply only bottom border */
		padding: 5px; /* Optional: Add padding */
		outline: none;
		/* font-size: 13px; */
	}
	.submit-btn {
		display: inline-block;
		background-color: #2c539e; /* Purple color */
		color: white;
		font-weight: bold;
		border: none;
		border-radius: 25px; /* Makes the button rounded */
		padding: 0.375rem 1.25rem;
		text-align: center;
		text-transform: uppercase; /* Make the text uppercase */
		cursor: pointer;
		transition: all 0.2s ease;
	}

	.submit-btn:hover {
		background-color: #1e3c78; /* Darken the button on hover */
		transform: scale(1.05); /* Slightly increase size on hover */
	}

	.submit-btn:active {
		background-color: #152a55; /* Darker on click */
		transform: scale(0.98); /* Shrink slightly on click */
	}

	.postcard {
		display: flex;
		justify-content: space-between;
		background-color: #fdfbf7;
		height: 95%;
	}

	.rubik {
		font-family: 'Ranille Normal', serif;
		/* font-size: 15px; */
	}
	.rubik-submit {
		font-family: 'Ranille Normal', serif;
		/* font-size: 12px; */
	}
	.rubik.purple {
		color: #2c539e;
	}
	/* .input-field {
		font-size: 13px;
	} */
	.checkbox-container {
		display: flex;
		align-items: flex-start;
		margin-top: 20px;
	}

	.checkbox-input {
		-webkit-appearance: none !important;
		appearance: none !important; /* Removes default checkbox styling */
		background-color: #fdfbf7 !important;
		padding: 0 !important;
		width: 13px;
		height: 13px;
		border: 2px solid #2c539e !important; /* Custom border color */
		border-radius: 4px;
		position: relative;
		cursor: pointer;
		transition: background-color 0.2s ease, border-color 0.2s ease;
		flex-shrink: 0;
		margin-top: 0.2em;
		outline: none !important;
	}

	.checkbox-input:checked {
		background-color: #2c539e !important;
		border-color: #2c539e !important;
	}

	.checkbox-input:checked::before {
		content: '✔';
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -59%);
		font-size: 14px;
		color: white;
	}

	.checkbox-label {
		margin-left: 10px;
		color: #535a5a;
		cursor: pointer; /* Makes the label clickable */
		font-family: 'Ranille Normal', serif;
	}

	.checkbox-input:focus {
		outline: 2px solid #2c539e;
		outline-offset: 2px;
	}

	.checkbox-input:hover {
		border-color: #1e3c78; /* Darker shade on hover */
	}

	/* MLH Agreement styling */
	.required-text {
		color: #d32f2f; /* Red color for required */
		font-weight: bold;
		font-size: 0.9em;
	}

	.optional-text {
		color: #1976d2; /* Blue color for optional */
		font-weight: bold;
		font-size: 0.9em;
	}

	.link-text {
		color: #2c539e; /* Purple color for links */
		text-decoration: underline;
		cursor: pointer;
	}

	.link-text:hover {
		color: #1e3c78; /* Darker purple on hover */
	}

	/* loading spinner */

	.lds-ripple,
	.lds-ripple div {
		box-sizing: border-box;
	}
	.lds-ripple {
		display: inline-block;
		position: relative;
		width: 80px;
		height: 80px;
	}
	.lds-ripple div {
		position: absolute;
		border: 4px solid #2c539e;
		opacity: 1;
		border-radius: 50%;
		animation: lds-ripple 1s cubic-bezier(0, 0.2, 0.8, 1) infinite;
	}
	.lds-ripple div:nth-child(2) {
		animation-delay: -0.5s;
	}
	@keyframes lds-ripple {
		0% {
			top: 36px;
			left: 36px;
			width: 8px;
			height: 8px;
			opacity: 0;
		}
		4.9% {
			top: 36px;
			left: 36px;
			width: 8px;
			height: 8px;
			opacity: 0;
		}
		5% {
			top: 36px;
			left: 36px;
			width: 8px;
			height: 8px;
			opacity: 1;
		}
		100% {
			top: 0;
			left: 0;
			width: 80px;
			height: 80px;
			opacity: 0;
		}
	}

	.popup-overlay {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, 0.5);
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 1000;
	}

	.popup-content {
		background: #fdfbf7;
		padding: 2rem;
		border-radius: 10px;
		box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
		max-width: 80%;
		text-align: center;
		border: 1px solid #d4c5a9;
	}
</style>
