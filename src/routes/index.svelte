<script context="module">
	export async function load({ page }) {
		const url = 'https://restcountries.com/v3.1/all';
		const res = await fetch(url);

		if (res.ok) {
			const data = await res.json();
			return {
				props: { data }
			};
		}

		return {
			status: res.status,
			error: new Error(`Could not load ${url}`)
		};
	}
</script>

<script>
	import { fade, scale } from 'svelte/transition';
	import Country from '../components/country.svelte';

	// states
	export let data;
	let searchQuery = '';
	let filteredCountries = [];
	let selected = '';

	// sorts data alphabetically
	const sortedCountry = data.sort((a, b) => a.name.common.localeCompare(b.name.common));

	$: {
		if (searchQuery) {
			// filter data baseed on the user input: search
			filteredCountries = sortedCountry.filter((country) =>
				country.name.common.toLowerCase().includes(searchQuery.toLowerCase())
			);
		} else if (selected) {
			// filter data based on user selected continent
			filteredCountries = sortedCountry.filter((country) =>
				country.region.toLowerCase().includes(selected.toLowerCase())
			);
		} else {
			filteredCountries = [...sortedCountry];
		}
	}
</script>

<svelte:head>
	<title>Rest Countries | Where in the world?</title>
</svelte:head>
<main class="text-[#111517] min-h-screen dark:bg-gray-900 dark:text-white">
	<div class="max-w-screen-xl m-auto px-3">
		<section class="pt-5">
			<div class="flex flex-col items-center justify-between lg:flex-row lg:pt-8">
				<form
					on:submit|preventDefault={() => console.log(searchQuery)}
					class="flex items-center h-12 px-6 rounded w-full box-shadow lg:w-[450px] bg-white dark:bg-gray-800"
					autocomplete="off"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						width="24"
						height="24"
						viewBox="0 0 24 24"
						fill="currentColor"
						class="leading-none"
						><path
							d="M10 18a7.952 7.952 0 0 0 4.897-1.688l4.396 4.396 1.414-1.414-4.396-4.396A7.952 7.952 0 0 0 18 10c0-4.411-3.589-8-8-8s-8 3.589-8 8 3.589 8 8 8zm0-14c3.309 0 6 2.691 6 6s-2.691 6-6 6-6-2.691-6-6 2.691-6 6-6z"
						/></svg
					>
					<input
						type="text"
						placeholder="Search for a country..."
						class="h-full w-full outline-none pl-4 text-[#858585] dark:bg-gray-800 dark:text-white"
						bind:value={searchQuery}
					/>
				</form>

				<select
					bind:value={selected}
					on:change={() => selected}
					class="bg-white flex items-center h-12 px-4 w-1/2 rounded box-shadow outline-none mt-12 self-start lg:mt-0 lg:w-max dark:bg-gray-800 dark:text-white"
				>
					<option value="">Filter by Region</option>
					<option value="africa">Africa</option>
					<option value="america">America</option>
					<option value="asia">Asia</option>
					<option value="europe">Europe</option>
					<option value="oceania">Oceania</option>
				</select>
			</div>
		</section>

		<section
			in:fade
			out:scale|local
			class="grid grid-cols-1 py-10 gap-10 w-64 m-auto sm:grid-cols-2 sm:w-[600px] md:grid-cols-3 md:w-full lg:py-14 xl:grid-cols-4 xl:gap-14"
		>
			{#each filteredCountries as country (country.name)}
				<Country {country} />
			{/each}
		</section>
	</div>
</main>

<style>
	.box-shadow {
		box-shadow: 0px 0.2px 1.7px rgba(0, 0, 0, 0.02), 0px 0.4px 4.2px rgba(0, 0, 0, 0.028),
			0px 0.8px 7.9px rgba(0, 0, 0, 0.035), 0px 1.3px 14.1px rgba(0, 0, 0, 0.042),
			0px 2.5px 26.3px rgba(0, 0, 0, 0.05), 0px 6px 63px rgba(0, 0, 0, 0.07);
	}
</style>
