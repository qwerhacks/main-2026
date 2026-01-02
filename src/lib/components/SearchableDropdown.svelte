<!-- SearchableDropdown.svelte -->
<script lang="ts">
	export let options: string[] = [];
	export let value: string = '';
	export let placeholder: string = 'Select an option';
	export let required: boolean = false;
	export let id: string = '';
	export let label: string = '';

	let isOpen = false;
	let searchTerm = '';
	let filteredOptions: string[] = [];

	$: {
		if (searchTerm === '') {
			filteredOptions = options;
		} else {
			filteredOptions = options.filter((option) =>
				option.toLowerCase().includes(searchTerm.toLowerCase())
			);
		}
	}

	function selectOption(option: string) {
		value = option;
		searchTerm = option;
		isOpen = false;
	}

	function handleInput(event: Event) {
		const target = event.target as HTMLInputElement;
		searchTerm = target.value;
		isOpen = true;
	}

	function handleBlur() {
		// Delay closing to allow for click events
		setTimeout(() => {
			isOpen = false;
		}, 200);
	}
</script>

<div class="dropdown-container">
	<label class="input-label rubik purple" for={id}>{label}</label>
	<div class="relative">
		<div>
			<input
				type="text"
				{id}
				bind:value={searchTerm}
				on:input={handleInput}
				on:blur={handleBlur}
				on:focus={() => (isOpen = true)}
				class="input-field spectral italic w-full input-underline"
				{placeholder}
				{required}
				autocomplete="off"
			/>
		</div>
		{#if isOpen && filteredOptions.length > 0}
			<div class="dropdown-list">
				{#each filteredOptions as option}
					<div class="dropdown-item" on:mousedown={() => selectOption(option)}>
						{option}
					</div>
				{/each}
			</div>
		{/if}
	</div>
</div>

<style>
	.dropdown-container {
		width: 100%;
		position: relative;
	}
	input::placeholder,
	.spectral {
		text-align: left;
		font-family: 'Spectral', serif;
		font-weight: 400;
		background: #fdfbf7;

		/* color: #9ca3a3; */
	}
	.dropdown-list {
		position: absolute;
		top: 100%;
		left: 0;
		right: 0;
		max-height: 200px;
		overflow-y: auto;
		background: #fdfbf7;
		border: 1px solid #2c539e;
		border-radius: 4px;
		z-index: 1000;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
		font-family: 'Spectral', serif;
		font-style: italic;
	}

	.dropdown-item {
		padding: 8px 12px;
		cursor: pointer;
		transition: background-color 0.2s;
		font-style: italic;
		font-family: 'Spectral', serif;
	}

	.dropdown-item:hover {
		background-color: #fdfbf7;
		font-family: 'Spectral', serif;
		font-style: italic;
	}

	/* Custom scrollbar for the dropdown list */
	.dropdown-list::-webkit-scrollbar {
		width: 6px;
		font-family: 'Spectral', serif;
	}

	.dropdown-list::-webkit-scrollbar-track {
		background: #fdfbf7;
		border-radius: 3px;
		font-family: 'Spectral', serif;
		font-style: italic;
	}

	.dropdown-list::-webkit-scrollbar-thumb {
		background: #2c539e;
		border-radius: 3px;
		font-family: 'Spectral', serif;
		font-style: italic;
	}

	.dropdown-list::-webkit-scrollbar-thumb:hover {
		background: #1e3c78;
	}
	.rubik {
		font-family: 'Ranille Normal', serif;
		/* font-size: 15px; */
	}

	@media (max-width: 400px) {
		.rubik {
			font-size: 9px;
		}
		.input-field, .dropdown-item {
			font-size: 9px;
		}
	}
	@media (min-width: 400px) {
		.rubik {
			font-size: 10px;
		}
		.input-field, .dropdown-item {
			font-size: 10px;
		}
	}
	@media (min-width: 500px) {
		.rubik {
			font-size: 10px;
		}
		.input-field, .dropdown-item {
			font-size: 10px;
		}
	}
	@media (min-width: 585px) {
		.rubik {
			font-size: 12px;
		}
		.input-field, .dropdown-item {
			font-size: 12px;
		}
	}
	@media (min-width: 768px) {
		.rubik {
			font-size: 13px;
		}
		.input-field, .dropdown-item {
			font-size: 13px;
		}
	}
	@media (min-width: 900px) {
		.rubik {
			font-size: 17px;
		}
		.input-field, .dropdown-item {
			font-size: 17px;
		}
	}
	@media (min-width: 1200px) {
		.rubik {
			font-size: 17px;
		}
		.input-field, .dropdown-item {
			font-size: 17px;
		}
	}
	@media (min-width: 1500px) {
		.rubik {
			font-size: 19px;
		}
		.input-field, .dropdown-item {
			font-size: 19px;
		}
	}
	@media (min-width: 1800px) {
		.rubik {
			font-size: 25px;
		}
		.input-field, .dropdown-item {
			font-size: 25px;
		}
	}
	@media (min-aspect-ratio: 5/7) and (max-aspect-ratio: 7/5) {
		.rubik {
			font-size: 1.9vw;
		}
		.input-field, .dropdown-item {
			font-size: 1.9vw;
		}
	}

	.rubik-submit {
		font-family: 'Ranille Normal', serif;
		/* font-size: 12px; */
	}
	.rubik.purple {
		color: #2c539e;
	}
	input.input-field {
		padding-left: 0.25rem;
	}
	.input-underline {
		border: none;
		border-bottom: 1px solid #bdbdbd;
		border-radius: 0;
		box-shadow: none;
	}
	.input-field,
	.dropdown-container input,
	select {
		/* font-size: 1rem !important; */
	}
	.dropdown-list,
	.dropdown-item {
		/* font-size: 1rem !important; */
	}
</style>
