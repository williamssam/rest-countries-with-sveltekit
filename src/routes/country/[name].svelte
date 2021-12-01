<script context="module">
	export async function load({ page }) {
		const url = `https://restcountries.com/v3.1/name/${page.params.name}?fullText=true`;

		const res = await fetch(url);
		const data = await res.json();

		return {
			props: { data }
		};
	}
</script>

<script>
	import CountryDetails from '../../components/countryDetails.svelte';
	export let data;

	const pageTitle = data[0].name.common;
</script>

<!-- renders country details page -->
<svelte:head>
	<title>{pageTitle} | Rest Countries</title>
</svelte:head>
<main class="px-6 font-nunito-sans min-h-screen dark:bg-gray-900 dark:text-white">
	<div class="py-8 lg:py-14 max-w-screen-xl m-auto">
		<a
			href="/"
			class="flex items-center justify-between gap-2 rounded box-shadow py-2 px-6 w-max dark:bg-gray-800"
		>
			<svg
				xmlns="http://www.w3.org/2000/svg"
				width="24"
				height="24"
				viewBox="0 0 24 24"
				fill="currentColor"
				><path
					d="M21 11H6.414l5.293-5.293-1.414-1.414L2.586 12l7.707 7.707 1.414-1.414L6.414 13H21z"
				/></svg
			>
			<span>Back</span>
		</a>

		{#each data as country (country.name.common)}
			<CountryDetails {country} />
		{/each}
	</div>
</main>

<style>
	.box-shadow {
		box-shadow: 0px 0.2px 1.7px rgba(0, 0, 0, 0.02), 0px 0.4px 4.2px rgba(0, 0, 0, 0.028),
			0px 0.8px 7.9px rgba(0, 0, 0, 0.035), 0px 1.3px 14.1px rgba(0, 0, 0, 0.042),
			0px 2.5px 26.3px rgba(0, 0, 0, 0.05), 0px 6px 63px rgba(0, 0, 0, 0.07);
	}
</style>
