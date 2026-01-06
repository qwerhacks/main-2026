<script lang="ts">
	//Postcard portion
	// import Textfield from '@smui/textfield';
	import { onMount } from 'svelte';
	import schoolsCsv from '$lib/media/schools.csv?raw';
	import countriesCsv from '$lib/media/slim-2.csv?raw';
	// import { SCRIPTS_API } from '$env/static/private';

	let isLoaded = false;

	onMount(() => {
		setTimeout(() => {
			isLoaded = true;
		}, 300);
	});

	// --- Form State ---
	let currentStep = 0;
	const totalSteps = 7;
	let error: string | undefined = undefined;
	let success: boolean = false;
	let loading: boolean = false;
	let showErrorPopup = false;
	let errorMessage = '';

	// --- Field Variables ---
	// Step 1: Welcome
	let missionSupport: string = ''; // Yes
	let accessibility: string = '';

	// Step 2: Personal Info
	let firstName: string = '';
	let lastName: string = '';
	let legalName: string = '';
	let studentEmail: string = ''; // This is the main email
	let phoneNumber: string = '';
	let age: string = '';
	let isUniversityStudent: string = ''; // Yes/No
	let hometown: string = '';
	let countryOfResidence: string = '';
	let raceEthnicity: string = '';
	let pronouns: string = '';
	let identity: string = '';

	// Step 3: Education
	let educationLevel: string = '';
	let school: string = '';
	let major: string = '';
	let gradYear: string = '';
	let degree: string = '';

	// Step 4: Links & Experience
	let github: string = '';
	let linkedinUrl: string = '';
	let firstHackathon: string = ''; // Yes/No
	let attendedBefore: string = ''; // Yes/No
	let workshops: string = '';
	let hearAbout: string = '';
	let buildIntent: string = '';
	let mentorship: string = ''; // Yes/No/Maybe

	// Step 5: Logistics
	let available: string = ''; // Yes/No/Maybe
	let computerAccess: string = ''; // Yes/No
	let carpooling: string = '';
	let dietary: string = '';

	// Step 6: Legal & Agreements
	let photoRelease: string = ''; // Yes/No
	let mlhPrivacy: boolean = false; // Yes
	let mlhEmails: string = ''; // Yes/No
	let codeOfConduct: boolean = false; // Yes
	let piiAck: boolean = false; // Yes
	let mlhTerms: boolean = false; // Yes
	let mlhPartners: string = ''; // Yes/No

	// Step 7: Wrap Up
	let referralName: string = '';
	let referralEmail: string = '';
	let excitement: string = '';
	let otherQuestions: string = '';

	// --- Options ---
	const studyLevels = [
		'First Year Undergraduate',
		'Second Year Undergraduate',
		'Third Year Undergraduate',
		'Fourth Year Undergraduate',
		'Fifth Year or Higher Undergraduate',
		'Graduate Student',
		'Finished Undergraduate within the last 6 months',
		'Received Graduate Degree within the last 6 months',
		'Other' // Mapped to empty string or "Other" in form? Form has "Other" option usually.
	];

	const gradYears = ['2025', '2026', '2027', '2028', 'Other'];
	const degrees = ['Associates', 'Bachelors', 'Masters', 'PhD', 'Other'];
	const yesNo = ['Yes', 'No'];
	const yesNoMaybe = ['Yes', 'No', 'Maybe'];
	const carpoolOptions = [
		'Yes, I can offer rides',
		'Yes, I’m looking for a ride',
		'Yes, I’m open to splitting an Uber/Lyft',
		'No, I’m not looking to carpool'
	];
	const excitementOptions = [
		'maximum excitement',
		'mAxImUm ExCiTeMeNt',
		'MaXiMuM eXcItEmEnT',
		'MAXIMUM EXCITEMENT'
	];

	const ageOptions = Array.from({ length: 90 }, (_, i) => (i + 10).toString());

	const schools = schoolsCsv
		.split('\n')
		.slice(1)
		.map((s) => s.trim())
		.filter((s) => s);

	const countries = countriesCsv
		.split('\n')
		.slice(1)
		.map((row) => {
			const parts = row.split(',');
			return parts[0] ? parts[0].trim() : '';
		})
		.filter((s) => s);

	// --- Navigation ---
	function nextStep() {
		if (validateStep(currentStep)) {
			currentStep++;
			error = undefined;
		}
	}

	function prevStep() {
		if (currentStep > 0) {
			currentStep--;
			error = undefined;
		}
	}

	function validateStep(step: number): boolean {
		// Simple validation: check if required fields are filled
		// You can add more specific validation (email regex, etc.) here
		let missing = [];

		if (step === 0) {
			if (!missionSupport) missing.push('Mission Support');
		} else if (step === 1) {
			if (!firstName) missing.push('First Name');
			if (!lastName) missing.push('Last Name');
			if (!legalName) missing.push('Legal Name');
			if (!studentEmail) missing.push('Student Email');
			if (!phoneNumber) missing.push('Phone Number');
			if (!age) missing.push('Age');
			if (!isUniversityStudent) missing.push('University Student Status');
			if (!hometown) missing.push('Hometown');
			if (!countryOfResidence) missing.push('Country of Residence');
			if (!raceEthnicity) missing.push('Race/Ethnicity');
			if (!pronouns) missing.push('Pronouns');
			// Identity is optional
		} else if (step === 2) {
			if (!educationLevel) missing.push('Education Level');
			if (!school) missing.push('School');
			if (!major) missing.push('Major');
			if (!gradYear) missing.push('Graduation Year');
			if (!degree) missing.push('Degree');
		} else if (step === 3) {
			// Github/Linkedin optional
			if (!firstHackathon) missing.push('First Hackathon');
			if (!attendedBefore) missing.push('Attended Before');
			if (!workshops) missing.push('Workshop Interests');
			if (!hearAbout) missing.push('How did you hear about us?');
			// Mentorship is optional
		} else if (step === 4) {
			if (!available) missing.push('Availability');
			if (!computerAccess) missing.push('Computer Access');
			// Carpooling is optional
		} else if (step === 5) {
			if (!photoRelease) missing.push('Photo Release');
			if (!mlhPrivacy) missing.push('MLH Privacy Policy');
			if (!mlhEmails) missing.push('MLH Emails');
			if (!codeOfConduct) missing.push('Code of Conduct');
			if (!piiAck) missing.push('PII Acknowledgement');
			if (!mlhTerms) missing.push('MLH Terms');
			// MLH Partners is optional
		} else if (step === 6) {
			// Excitement is optional
		}

		if (missing.length > 0) {
			errorMessage = `Please fill in: ${missing.join(', ')}`;
			showErrorPopup = true;
			return false;
		}
		return true;
	}

	function closePopup() {
		showErrorPopup = false;
	}

	// --- Submission ---
	async function submitHandler(e: Event) {
		loading = true;
		error = undefined;
		success = false;

		// Final validation
		if (!validateStep(currentStep)) {
			loading = false;
			return;
		}

		const GOOGLE_FORM_URL =
			'https://docs.google.com/forms/u/0/d/e/1FAIpQLSfWmQDnkrIx32-oQlLF6Y4ucjvX7JUtfnNSwMgA0Xt-7M9mAQ/formResponse';

		const formData = new FormData();
		
		// Step 1
		formData.append('entry.240838994', missionSupport);
		formData.append('entry.2092845830', accessibility);

		// Step 2
		formData.append('entry.1881511310', firstName);
		formData.append('entry.1806032634', lastName);
		formData.append('entry.162840080', legalName);
		formData.append('emailAddress', studentEmail); // Special field
		formData.append('entry.1809332349', studentEmail); // Also as entry? Usually just emailAddress for collected email.
		formData.append('entry.130050569', phoneNumber);
		formData.append('entry.643094675', age);
		formData.append('entry.656549759', isUniversityStudent);
		formData.append('entry.185093171', hometown);
		formData.append('entry.841235035', countryOfResidence);
		formData.append('entry.840849010', raceEthnicity);
		formData.append('entry.1337251263', pronouns);
		formData.append('entry.917043067', identity);

		// Step 3
		formData.append('entry.1390694085', educationLevel);
		formData.append('entry.2115360662', school);
		formData.append('entry.674608404', major);
		formData.append('entry.1889976980', gradYear);
		formData.append('entry.1110266826', degree);

		// Step 4
		formData.append('entry.1700342900', github);
		formData.append('entry.1731926023', linkedinUrl);
		formData.append('entry.2135533020', firstHackathon);
		formData.append('entry.214856401', attendedBefore);
		formData.append('entry.1286763055', workshops);
		formData.append('entry.1421523047', hearAbout);
		formData.append('entry.1625026120', buildIntent);
		formData.append('entry.1371002818', mentorship);

		// Step 5
		formData.append('entry.1033312778', available);
		formData.append('entry.846262195', computerAccess);
		formData.append('entry.1355871345', carpooling);
		formData.append('entry.1768185081', dietary);

		// Step 6
		formData.append('entry.2018743103', photoRelease);
		formData.append('entry.2045840030', mlhPrivacy ? 'Yes' : '');
		formData.append('entry.75398305', mlhEmails);
		formData.append('entry.1210042134', codeOfConduct ? 'Yes' : '');
		formData.append('entry.766993469', piiAck ? 'Yes' : '');
		formData.append('entry.1718472215', mlhTerms ? 'Yes' : '');
		formData.append('entry.1640257796', mlhPartners);

		// Step 7
		formData.append('entry.436027630', referralName);
		formData.append('entry.1099327287', referralEmail);
		formData.append('entry.1812241421', excitement);
		formData.append('entry.163027846', otherQuestions);

		// Debug: Log all entries to verify data before sending
		console.log('Form Data to be sent:');
		for (const pair of formData.entries()) {
			console.log(`${pair[0]}: ${pair[1]}`);
		}

		console.log('Sending to Google Form');

		try {
			await fetch(GOOGLE_FORM_URL, {
				method: 'POST',
				mode: 'no-cors',
				body: formData
			});

			success = true;
			console.log('Form submitted successfully (no-cors mode)');
		} catch (err) {
			console.error('Network error:', err);
			error = err instanceof Error ? err.message : 'Unknown error';
		} finally {
			loading = false;
		}
	}
	// Apply now
	function openApplicationForm() {
		window.open('https://tinyurl.com/qwerhacks25', '_blank');
	}
</script>

<div class="container">
	{#if true}
		<div class="scroll-paper {isLoaded ? 'slide-in' : 'slide-out'}">
			<div
				class="scroll-content"
				aria-label="RSVP form. fill in your information here to register."
			>
				<!-- <img src={Back} alt="postcard back" /> -->
				<div class="postcard">
					<!-- Right side: Sign-up form -->
					<div class="right">
						<!-- <img
							src={Updates}
							alt="Sign up for Updates!"
							class="updates"
							style="visibility: hidden;"
						/> -->
						<form on:submit|preventDefault={submitHandler}>
							{#if error === undefined && !success}
								<div class="input-group flex-col flex">
									<label class="input-label rubik purple"
										><span style="font-size: 1.5em;">Application Form</span></label
									>
									<p class="spectral italic text-sm text-gray-500 mb-4">Step {currentStep + 1} of {totalSteps}</p>
								</div>

								<!-- Step 0: Welcome -->
								{#if currentStep === 0}
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="missionSupport">Do you support the mission of QWER Hacks?*</label>
										<select id="missionSupport" bind:value={missionSupport} class="input-field spectral italic w-full" required>
											<option value="" disabled selected>Select...</option>
											{#each yesNo as opt}
												<option value={opt}>{opt}</option>
											{/each}
										</select>
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="accessibility">Do you require any accessibility accommodations we can help provide?</label>
										<input type="text" id="accessibility" bind:value={accessibility} class="input-field spectral italic w-full" placeholder="Any accommodations?" />
									</div>
								{/if}

								<!-- Step 1: Personal Info -->
								{#if currentStep === 1}
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="firstName">Hi! What's your preferred first name?*</label>
										<input type="text" id="firstName" bind:value={firstName} class="input-field spectral italic w-full" required />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="lastName">What's your last name?*</label>
										<input type="text" id="lastName" bind:value={lastName} class="input-field spectral italic w-full" required />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="legalName">Please provide your full legal name in (Last, First) format*</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">We unfortunately have to collect this information for liability reasons.</p>
										<input type="text" id="legalName" bind:value={legalName} class="input-field spectral italic w-full" required />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="studentEmail">What's your student email (*.edu)?*</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">Please reach out to the organizers at qwerhacks@gmail.com if you are a university student but do not have a university email that ends in .edu</p>
										<input type="email" id="studentEmail" bind:value={studentEmail} class="input-field spectral italic w-full" required />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="phoneNumber">What's your phone number?*</label>
										<input type="tel" id="phoneNumber" bind:value={phoneNumber} class="input-field spectral italic w-full" required />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="age">What is your age?*</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">You must be 18 years of age or older to attend QWER Hacks.</p>
										<select id="age" bind:value={age} class="input-field spectral italic w-full" required>
											<option value="" disabled selected>Select Age</option>
											{#each ageOptions as opt}
												<option value={opt}>{opt}</option>
											{/each}
										</select>
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="isUniversityStudent">Are you a university student?*</label>
										<select id="isUniversityStudent" bind:value={isUniversityStudent} class="input-field spectral italic w-full" required>
											<option value="" disabled selected>Select...</option>
											{#each yesNo as opt}
												<option value={opt}>{opt}</option>
											{/each}
										</select>
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="hometown">Where are you from?*</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">e.g. Los Angeles, California. Note: QWER Hacks 2026 will only be available for in-person attendance</p>
										<input type="text" id="hometown" bind:value={hometown} class="input-field spectral italic w-full" required />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="countryOfResidence">What is your country of residence?*</label>
										<input list="countries-list" id="countryOfResidence" bind:value={countryOfResidence} class="input-field spectral italic w-full" placeholder="Select Country" required />
										<datalist id="countries-list">
											{#each countries as country}
												<option value={country} />
											{/each}
										</datalist>
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="raceEthnicity">What is your race or ethnicity?*</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">e.g. Southeast Asian, Black, African American, Colombian, etc.</p>
										<input type="text" id="raceEthnicity" bind:value={raceEthnicity} class="input-field spectral italic w-full" required />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="pronouns">Please share the pronouns you would like to use in this space.*</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">e.g. they/them/theirs. Find more information here: https://lgbtlifecenter.org/pronouns/ Please indicate your pronouns (multiple choices are allowed). This data is collected only for hackathon planning purposes, and will be kept confidential. It is purely optional and will be de-associated from your personal information.</p>
										<input type="text" id="pronouns" bind:value={pronouns} class="input-field spectral italic w-full" required />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="identity">How do you identify?</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">e.g. pansexual, demigirl, ally</p>
										<input type="text" id="identity" bind:value={identity} class="input-field spectral italic w-full" />
									</div>
								{/if}

								<!-- Step 2: Education -->
								{#if currentStep === 2}
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="educationLevel">What is your current level of education?*</label>
										<select id="educationLevel" bind:value={educationLevel} class="input-field spectral italic w-full" required>
											<option value="" disabled selected>Select Level</option>
											{#each studyLevels as level}
												<option value={level}>{level}</option>
											{/each}
										</select>
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="school">What school are you currently enrolled in?*</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">Please write out the full name of your school. For example, write University of California, Los Angeles - not UCLA! If you are not currently in school, please briefly explain what opportunities you're pursuing.</p>
										<input list="schools-list" id="school" bind:value={school} class="input-field spectral italic w-full" placeholder="Select School" required />
										<datalist id="schools-list">
											{#each schools as s}
												<option value={s} />
											{/each}
										</datalist>
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="major">What is your major?*</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">Please write out the full name of your major. For example, write Computer Science and Engineering - not CSE! If you are not currently in school, please list what fields you're passionate about.</p>
										<input type="text" id="major" bind:value={major} class="input-field spectral italic w-full" required />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="gradYear">What is your expected graduation year?*</label>
										<select id="gradYear" bind:value={gradYear} class="input-field spectral italic w-full" required>
											<option value="" disabled selected>Select Year</option>
											{#each gradYears as year}
												<option value={year}>{year}</option>
											{/each}
										</select>
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="degree">What degree are you currently pursuing?*</label>
										<select id="degree" bind:value={degree} class="input-field spectral italic w-full" required>
											<option value="" disabled selected>Select Degree</option>
											{#each degrees as d}
												<option value={d}>{d}</option>
											{/each}
										</select>
									</div>
								{/if}

								<!-- Step 3: Links & Experience -->
								{#if currentStep === 3}
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="github">What is your GitHub username?</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">Will be shared with our sponsors.</p>
										<input type="url" id="github" bind:value={github} class="input-field spectral italic w-full" />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="linkedinUrl">What is your LinkedIn link/profile?</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">Will be shared with our sponsors. Make sure your link starts with "http:// " or "https://", or google forms won't accept your link!</p>
										<input type="url" id="linkedinUrl" bind:value={linkedinUrl} class="input-field spectral italic w-full" />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="firstHackathon">Is this your first hackathon?*</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">It's totally okay if it is! We love supporting first time attendees :)</p>
										<select id="firstHackathon" bind:value={firstHackathon} class="input-field spectral italic w-full" required>
											<option value="" disabled selected>Select...</option>
											{#each yesNo as opt}
												<option value={opt}>{opt}</option>
											{/each}
										</select>
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="attendedBefore">Have you attended QWER Hacks before?*</label>
										<select id="attendedBefore" bind:value={attendedBefore} class="input-field spectral italic w-full" required>
											<option value="" disabled selected>Select...</option>
											{#each yesNo as opt}
												<option value={opt}>{opt}</option>
											{/each}
										</select>
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="workshops">List technical workshop(s) you would like to see*</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">e.g. deep learning, web development, UI/UX, etc.</p>
										<input type="text" id="workshops" bind:value={workshops} class="input-field spectral italic w-full" required />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="hearAbout">How did you hear about QWER Hacks?*</label>
										<input type="text" id="hearAbout" bind:value={hearAbout} class="input-field spectral italic w-full" required />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="buildIntent">What would you like to build at QWER Hacks?</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">We highly encourage engineering products that benefit underrepresented groups in STEM, but if you don't know yet that's okay too!!</p>
										<input type="text" id="buildIntent" bind:value={buildIntent} class="input-field spectral italic w-full" />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="mentorship">Are you interested in identity-specific mentorship groups?</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">These groups will give you the opportunity to network with company representatives, mentors, and other hackers who share your identity. Ex: Bi/Pan mentorship group, TGNC mentorship group</p>
										<select id="mentorship" bind:value={mentorship} class="input-field spectral italic w-full">
											<option value="" disabled selected>Select...</option>
											{#each yesNoMaybe as opt}
												<option value={opt}>{opt}</option>
											{/each}
										</select>
									</div>
								{/if}

								<!-- Step 4: Logistics -->
								{#if currentStep === 4}
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="available">Are you available February 7-8, 2026? We will be in-person at the Palisades Room in Carnesale Commons!*</label>
										<select id="available" bind:value={available} class="input-field spectral italic w-full" required>
											<option value="" disabled selected>Select...</option>
											{#each yesNoMaybe as opt}
												<option value={opt}>{opt}</option>
											{/each}
										</select>
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="computerAccess">Do you have stable access to a computer?*</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">Totally okay if not! We just want to be able to support you.</p>
										<select id="computerAccess" bind:value={computerAccess} class="input-field spectral italic w-full" required>
											<option value="" disabled selected>Select...</option>
											{#each yesNo as opt}
												<option value={opt}>{opt}</option>
											{/each}
										</select>
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="carpooling">Are you open to carpooling with other attendees?</label>
										<select id="carpooling" bind:value={carpooling} class="input-field spectral italic w-full">
											<option value="" disabled selected>Select...</option>
											{#each carpoolOptions as opt}
												<option value={opt}>{opt}</option>
											{/each}
										</select>
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="dietary">Please list any dietary restrictions or allergies you have.</label>
										<p class="spectral italic text-sm text-gray-500 mb-2">If you don't have any, skip this question :)</p>
										<input type="text" id="dietary" bind:value={dietary} class="input-field spectral italic w-full" />
									</div>
								{/if}

								<!-- Step 5: Legal -->
								{#if currentStep === 5}
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="photoRelease">I hereby grant permission to UCLA, SWE, MLH, and QWER Hacks to use photographs and/or video of me taken on February 7th-8th, 2026 at UCLA in publications, news releases, online and in other communications related to the mission of QWER Hacks.*</label>
										<select id="photoRelease" bind:value={photoRelease} class="input-field spectral italic w-full" required>
											<option value="" disabled selected>Select...</option>
											{#each yesNo as opt}
												<option value={opt}>{opt}</option>
											{/each}
										</select>
									</div>
									<div class="checkbox-container">
										<input type="checkbox" bind:checked={mlhPrivacy} id="mlhPrivacy" class="checkbox-input" required />
										<label for="mlhPrivacy" class="checkbox-label">
											<span class="text-red-500">*</span> I authorize you to share my application/registration information with Major League Hacking for event administration, ranking, and MLH administration in-line with the <a href="https://mlh.io/privacy" target="_blank" class="link-text">MLH Privacy Policy</a>. I further agree to the terms of both the <a href="https://github.com/MLH/mlh-policies/blob/main/contest-terms.md" target="_blank" class="link-text">MLH Contest Terms and Conditions</a> and the <a href="https://mlh.io/privacy" target="_blank" class="link-text">MLH Privacy Policy</a>.
										</label>
									</div>
									<div class="input-group flex-col flex mt-4">
										<label class="input-label rubik purple" for="mlhEmails">I authorize MLH to send me an email where I can further opt into the MLH Hacker, Events, or Organizer Newsletters and other communications from MLH.*</label>
										<select id="mlhEmails" bind:value={mlhEmails} class="input-field spectral italic w-full" required>
											<option value="" disabled selected>Select...</option>
											{#each yesNo as opt}
												<option value={opt}>{opt}</option>
											{/each}
										</select>
									</div>
									<div class="checkbox-container">
										<input type="checkbox" bind:checked={codeOfConduct} id="codeOfConduct" class="checkbox-input" required />
										<label for="codeOfConduct" class="checkbox-label">
											<span class="text-red-500">*</span> I have read and agree to the <a href="https://static.mlh.io/docs/mlh-code-of-conduct.pdf" target="_blank" class="link-text">QWER Hacks Code of Conduct</a>.
										</label>
									</div>
									<div class="checkbox-container">
										<input type="checkbox" bind:checked={piiAck} id="piiAck" class="checkbox-input" required />
										<label for="piiAck" class="checkbox-label">
											<span class="text-red-500">*</span> I acknowledge that QWER Hacks will never disclose or disseminate any personally identifiable information (including, but not limited to, name, email address, phone number, Github, LinkedIn, resume, and emergency contact information) to any individuals or parties, with the exception of event organizers, company sponsors, and Major League Hacking, without permission. Additionally, all information and statistics related to QWER Hacks released to UCLA and the general public will be aggregated and stripped of any personally identifiable information.
										</label>
									</div>
									<div class="checkbox-container">
										<input type="checkbox" bind:checked={mlhTerms} id="mlhTerms" class="checkbox-input" required />
										<label for="mlhTerms" class="checkbox-label">
											<span class="text-red-500">*</span> I authorize you to share my application/registration information with Major League Hacking for event administration, ranking, and MLH administration in-line with the <a href="https://mlh.io/privacy" target="_blank" class="link-text">MLH Privacy Policy</a>. I further agree to the terms of both the <a href="https://github.com/MLH/mlh-policies/blob/main/contest-terms.md" target="_blank" class="link-text">MLH Contest Terms and Conditions</a> and the <a href="https://mlh.io/privacy" target="_blank" class="link-text">MLH Privacy Policy</a>.
										</label>
									</div>
									<div class="input-group flex-col flex mt-4">
										<label class="input-label rubik purple" for="mlhPartners">I authorize MLH to send me pre- and post-event informational emails, which contain free credit and opportunities from their partners.</label>
										<select id="mlhPartners" bind:value={mlhPartners} class="input-field spectral italic w-full">
											<option value="" disabled selected>Select...</option>
											{#each yesNo as opt}
												<option value={opt}>{opt}</option>
											{/each}
										</select>
									</div>
								{/if}

								<!-- Step 6: Wrap Up -->
								{#if currentStep === 6}
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="referralName">What is the name of the person who referred you? (first and last)</label>
										<input type="text" id="referralName" bind:value={referralName} class="input-field spectral italic w-full" />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="referralEmail">What is the email of the person who referred you?</label>
										<input type="email" id="referralEmail" bind:value={referralEmail} class="input-field spectral italic w-full" />
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="excitement">How excited are you for QWER Hacks?</label>
										<select id="excitement" bind:value={excitement} class="input-field spectral italic w-full">
											<option value="" disabled selected>Select...</option>
											{#each excitementOptions as opt}
												<option value={opt}>{opt}</option>
											{/each}
										</select>
									</div>
									<div class="input-group flex-col flex">
										<label class="input-label rubik purple" for="otherQuestions">Any other questions, comments, concerns?</label>
										<input type="text" id="otherQuestions" bind:value={otherQuestions} class="input-field spectral italic w-full" />
									</div>
								{/if}

								<!-- Navigation Buttons -->
								<div class="w-full flex justify-between items-center mt-6">
									{#if currentStep > 0}
										<button type="button" on:click={prevStep} class="submit-btn rubik-submit">Back</button>
									{:else}
										<div></div>
									{/if}

									{#if currentStep < totalSteps - 1}
										<button type="button" on:click={nextStep} class="submit-btn rubik-submit">Next</button>
									{:else}
										{#if !loading}
											<button type="submit" class="submit-btn rubik-submit">Submit</button>
										{:else}
											<div class="lds-ripple"><div></div><div></div></div>
										{/if}
									{/if}
								</div>

							{:else if success}
								<div>
									<p class="text-center spectral italic text-grey text-m">
										Thank you! Your application has been submitted successfully. Please keep an eye on your email for more info.
									</p>
								</div>
							{:else}
								<div>
									<p class="text-center spectral italic text-grey text-m">
										Error encountered. Please reload and try again.
									</p>
								</div>
								<div class="max-h-[7ch] overflow-scroll text-red-500">Error: {error}</div>
							{/if}
						</form>
					</div>
				</div>
			</div>
		</div>
	{:else}
		<p class="text-center spectral italic text-white text-[2.5vw]">
			Our server is currently experiencing difficulties. We seek your understanding and patience as
			we fix the issues. Kindly visit our page again later. We apologize for any inconvenience
			caused.
		</p>
	{/if}
</div>

	{#if showErrorPopup}
		<div class="popup-overlay">
			<div class="popup-content">
				<h3 class="rubik purple" style="font-size: 1.5em; margin-bottom: 10px;">Incomplete Fields</h3>
				<p class="spectral italic text-grey text-m" style="margin-bottom: 20px;">{errorMessage}</p>
				<button class="submit-btn rubik-submit" on:click={closePopup}>OK</button>
			</div>
		</div>
	{/if}

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
		aspect-ratio: 500/354;
		/* min-height: auto; */
		perspective: 800px;
	}

	@media (max-width: 400px) {
		/* Target small screens like phones */
		.container {
			width: 90%;
		}
		.overlay-text {
			font-size: 12px;
		}
		.rubik {
			font-size: 9px;
		}
		.input-field {
			font-size: 9px;
		}
		.address {
			font-size: 8px;
		}
		.rubik-submit {
			font-size: 8px;
		}
		.checkbox-label {
			font-size: 8px;
		}
	}
	@media (min-width: 400px) {
		/* Target small screens like phones */
		.container {
			width: 80%;
		}
		.overlay-text {
			font-size: 17px;
		}
		.rubik {
			font-size: 10px;
		}
		.input-field {
			font-size: 10px;
		}
		.address {
			font-size: 9px;
		}
		.rubik-submit {
			font-size: 8px;
		}
		.checkbox-label {
			font-size: 9px;
		}
	}
	@media (min-width: 500px) {
		/* Target small screens like phones */
		.container {
			width: 85%;
		}
		.overlay-text {
			font-size: 22px;
		}
		.rubik {
			font-size: 10px;
		}
		.rubik-submit {
			font-size: 10px;
		}
		.input-field {
			font-size: 10px;
		}
		.checkbox-label {
			font-size: 10px;
		}
	}
	@media (min-width: 585px) {
		.container {
			width: 80%; /* Narrower width */
		}
		.overlay-text {
			font-size: 26px;
		}
		.rubik {
			font-size: 12px;
		}
		.input-field {
			font-size: 12px;
		}
		.address {
			font-size: 11px;
		}
		.checkbox-label {
			font-size: 12px;
		}
	}
	@media (min-width: 768px) {
		.container {
			width: 75%; /* Narrower width */
		}
		.overlay-text {
			font-size: 26px;
		}
		.rubik-submit {
			font-size: 14px;
		}
		.rubik {
			font-size: 13px;
		}
		.input-field {
			font-size: 13px;
		}
		.checkbox-label {
			font-size: 12px;
		}
	}
	/* Extra-large screens (min-width: 1200px) */
	@media (min-width: 900px) {
		.container {
			width: 60%; /* Narrow width for big screens */
		}
		.overlay-text {
			font-size: 27px;
		}
		.rubik-submit {
			font-size: 14px;
		}
		.rubik {
			font-size: 17px;
		}
		.input-field {
			font-size: 17px;
		}
		.checkbox-label {
			font-size: 12px;
		}
	}
	@media (min-width: 1200px) {
		.container {
			width: 60%; /* Narrow width for big screens */
		}
		.overlay-text {
			font-size: 27px;
		}
		.rubik-submit {
			font-size: 16px;
		}
		.rubik {
			font-size: 17px;
		}
		.input-field {
			font-size: 17px;
		}
		.checkbox-label {
			font-size: 14px;
		}
	}
	@media (min-width: 1500px) {
		.container {
			width: 60%; /* Narrow width for big screens */
		}
		.overlay-text {
			font-size: 27px;
		}
		.rubik-submit {
			margin-top: 10px;
			font-size: 18px;
		}
		.rubik {
			font-size: 19px;
		}
		.input-field {
			font-size: 19px;
		}
		.checkbox-label {
			font-size: 15px;
		}
	}
	@media (min-width: 1800px) {
		.container {
			width: 60%; /* Narrow width for big screens */
		}
		.overlay-text {
			font-size: 27px;
		}
		.rubik-submit {
			margin-top: 20px;
			font-size: 20px;
		}
		.rubik {
			font-size: 25px;
		}
		.input-field {
			font-size: 25px;
		}
		.checkbox-label {
			font-size: 17px;
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
		align-items: center;
		margin-top: 20px;
	}

	.checkbox-input {
		appearance: none; /* Removes default checkbox styling */
		width: 13px;
		height: 13px;
		border: 2px solid #2c539e; /* Custom border color */
		border-radius: 4px;
		position: relative;
		cursor: pointer;
		transition: background-color 0.2s ease, border-color 0.2s ease;
	}

	.checkbox-input:checked {
		background-color: #2c539e;
		border-color: #2c539e;
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
