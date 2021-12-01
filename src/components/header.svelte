<script>
	const toggleDarkMode = () => {
		document.body.classList.toggle('dark');
	};
</script>

<header
	class="font-nunito-sans py-5 px-2 box-shadow text-[#111517] dark:bg-gray-800 dark:text-white"
>
	<div class="max-w-screen-xl m-auto px-3">
		<nav class="flex items-center justify-between">
			<h2 class="font-extrabold text-base md:text-xl lg:text-2xl">
				<a href="/">Where in the world?</a>
			</h2>
			<button class="flex items-center gap-2 p-2" on:click={() => toggleDarkMode()}>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					width="16"
					height="16"
					viewBox="0 0 24 24"
					fill="currentColor"
					><path
						d="M20.742 13.045a8.088 8.088 0 0 1-2.077.271c-2.135 0-4.14-.83-5.646-2.336a8.025 8.025 0 0 1-2.064-7.723A1 1 0 0 0 9.73 2.034a10.014 10.014 0 0 0-4.489 2.582c-3.898 3.898-3.898 10.243 0 14.143a9.937 9.937 0 0 0 7.072 2.93 9.93 9.93 0 0 0 7.07-2.929 10.007 10.007 0 0 0 2.583-4.491 1.001 1.001 0 0 0-1.224-1.224zm-2.772 4.301a7.947 7.947 0 0 1-5.656 2.343 7.953 7.953 0 0 1-5.658-2.344c-3.118-3.119-3.118-8.195 0-11.314a7.923 7.923 0 0 1 2.06-1.483 10.027 10.027 0 0 0 2.89 7.848 9.972 9.972 0 0 0 7.848 2.891 8.036 8.036 0 0 1-1.484 2.059z"
					/></svg
				>
				<span class="font-semibold text-xs lg:text-sm">Dark Mode</span>
			</button>
		</nav>
	</div>
</header>

<style>
	.box-shadow {
		box-shadow: 0px 0.2px 1.7px rgba(0, 0, 0, 0.02), 0px 0.4px 4.2px rgba(0, 0, 0, 0.028),
			0px 0.8px 7.9px rgba(0, 0, 0, 0.035), 0px 1.3px 14.1px rgba(0, 0, 0, 0.042),
			0px 2.5px 26.3px rgba(0, 0, 0, 0.05), 0px 6px 63px rgba(0, 0, 0, 0.07);
	}
</style>
