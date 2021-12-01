<script>
	import data from '../utils/countryCode.json';
	export let country;

	// converts ISO-3 code returned by the api to the full country name
	function getCode(code) {
		const countryCode = data
			.map((c) => (c.code === code ? c.name : null))
			.join(' ')
			.trim();

		return countryCode;
	}

	const nativeName = Object.values(country.name.nativeName).find((native) => native);
</script>

<!-- renders individual country details -->
{#if !country}
	<h2>Loading...</h2>
{:else}
	<article class="pt-16 lg:grid lg:grid-cols-2 lg:gap-10 lg:pt-20 xl:gap-24">
		<img src={country.flags.svg} alt={country.name.common} class="shadow-md" />

		<div class="pt-8 xl:flex xl:flex-col xl:justify-between xl:p-0">
			<div>
				<h2 class="font-bold text-lg lg:text-2xl">{country.name.common}</h2>

				<div class="sm:flex sm:justify-between">
					<ul class="pt-5 flex flex-col gap-1 xl:gap-2">
						<li>
							<strong class="font-semibold">Native Name:</strong>
							{nativeName.common}
						</li>
						<li>
							<strong class="font-semibold">Population:</strong>
							{country.population.toLocaleString()}
						</li>
						<li><strong class="font-semibold">Region:</strong> {country.region}</li>
						<li><strong class="font-semibold">Sub Region:</strong> {country.subregion}</li>
						<li><strong class="font-semibold">Capital:</strong> {country.capital[0] ?? ''}</li>
					</ul>

					<ul class="pt-10 flex flex-col gap-1 sm:pt-5 xl:gap-2">
						<li><strong class="font-semibold">Area:</strong> {country.area.toLocaleString()} sq</li>
						<li><strong class="font-semibold">Top Level Domain:</strong> {country.tld[0]}</li>
						<li>
							<strong class="font-semibold">Currency:</strong>
							{Object.values(country.currencies)
								.map((h) => `${h.name} (${h.symbol})`)
								.join(', ')}
						</li>
						<li>
							<strong class="font-semibold">Language:</strong>
							{Object.values(country.languages).join(', ')}
						</li>
					</ul>
				</div>
			</div>

			<div class="pt-10 sm:flex sm:items-center sm:flex-auto sm:gap-4 lg:pt-2">
				<h3 class="font-semibold">Border Countries:</h3>

				<div class="flex items-center flex-wrap gap-4 py-5 text-sm ">
					{#if country?.borders}
						{#each country?.borders as borderCountry}
							<a
								href={`/country/${getCode(borderCountry).toLowerCase()}`}
								class="py-1 px-5 rounded box-shadow dark:bg-gray-800">{getCode(borderCountry)}</a
							>
						{/each}
					{/if}
				</div>
			</div>
		</div>
	</article>
{/if}

<style>
	.box-shadow {
		box-shadow: 0px 0.2px 1.7px rgba(0, 0, 0, 0.02), 0px 0.4px 4.2px rgba(0, 0, 0, 0.028),
			0px 0.8px 7.9px rgba(0, 0, 0, 0.035), 0px 1.3px 14.1px rgba(0, 0, 0, 0.042),
			0px 2.5px 26.3px rgba(0, 0, 0, 0.05), 0px 6px 63px rgba(0, 0, 0, 0.07);
	}
</style>
