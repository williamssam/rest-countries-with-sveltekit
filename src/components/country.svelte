<script>
	export let country;
</script>

<!-- renders individual country card on the homepage -->
<article class="bg-white font-nunito-sans rounded-md box-shadow overflow-hidden dark:bg-gray-800">
	<a sveltekit:prefetch href={`/country/${country.name.common.toLowerCase()}`}>
		<img src={country.flags.svg} alt={country.name} class="h-40 w-full object-cover" />

		<div class="px-6 py-5">
			<h2 class="font-bold text-lg">{country?.name?.common}</h2>

			<ul class="py-3 text-sm flex flex-col gap-1">
				<li>
					<strong class="font-semibold">Population:</strong>
					{country.population.toLocaleString()}
				</li>
				<li><strong class="font-semibold">Region:</strong> {country.region}</li>
				<li><strong class="font-semibold">Capital:</strong> {country.capital?.[0] ?? ''}</li>
			</ul>
		</div>
	</a>
</article>

<style>
	.box-shadow {
		box-shadow: 0px 0.2px 1.7px rgba(0, 0, 0, 0.02), 0px 0.4px 4.2px rgba(0, 0, 0, 0.028),
			0px 0.8px 7.9px rgba(0, 0, 0, 0.035), 0px 1.3px 14.1px rgba(0, 0, 0, 0.042),
			0px 2.5px 26.3px rgba(0, 0, 0, 0.05), 0px 6px 63px rgba(0, 0, 0, 0.07);
	}
</style>
