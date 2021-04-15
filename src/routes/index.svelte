<script>
	import Lightspeed from '$lib/Lightspeed.svelte';

	let lightspeedComponent;

	function register() {
		lightspeedComponent.activateLightspeed();
		setTimeout(() => {
			window.location = 'https://share.hsforms.com/1Iatqi8VMQ1-PHI6uDnd7TQ1swik';
		}, 3000);
	}
	function info(event) {
		lightspeedComponent.activateLightspeed();
		setTimeout(() => {
			window.location = event.target.href;
		}, 3000);
	}
</script>

<svelte:head>
	<meta property="og:title" content="Looker at Lightspeed ⚡️" />
	<meta
		property="og:description"
		content="Data visualisation meets DevOps － an online event presented by Servian and Looker."
	/>
	<meta property="og:url" content="https://www.lightspeed.builders" />
	<meta property="og:image" content="/preview.jpg" />
	<meta name="twitter:card" content="summary_large_image" />
	<meta name="twitter:site" content="@WeAreServian" />
	<meta name="twitter:creator" content="@chistippett_" />
	<title>Looker at Lightspeed</title>
</svelte:head>

<Lightspeed bind:this={lightspeedComponent} />
<main>
	<div class="fixed inset-0 flex flex-col items-center justify-center text-white">
		<div class="">
			<img class="h-8 lg:h-10" src="/img/servian.svg" alt="Servian" />
		</div>
		<div class="mt-3">
			<div class="-mt-4 -ml-6 flex flex-wrap justify-between">
				<div class="mt-4 ml-6 flex flex-grow flex-shrink-0 lg:flex-grow-0">
					<img class="h-4 lg:h-6" src="/img/googlecloud.svg" alt="Tuple" />
				</div>
				<div class="mt-4 ml-6 flex flex-grow flex-shrink-0 lg:flex-grow-0">
					<img class="h-4 lg:h-6" src="/img/looker.svg" alt="Mirage" />
				</div>
				<div class="mt-4 ml-6 flex flex-grow flex-shrink-0 lg:flex-grow-0">
					<img class="h-4 lg:h-6" src="/img/hashicorp.svg" alt="Transistor" />
				</div>
			</div>
		</div>

		<div class="font-light text-sm mt-4 mb-10">Present</div>

		<div>
			<img class="h-24 lg:h-36" src="/img/title.svg" alt="Looker at Lightspeed" />
		</div>

		<div class="tracking-wider flex flex-col items-center mt-6">
			<div class="font-light  text-md">Tuesday, April 20 2021</div>
			<div class="font-semibold">2 – 3pm <span class="text-xs font-normal">GMT</span></div>
		</div>

		<button
			on:click={register}
			class="font-mont text-xl lg:text-2xl bg-white rounded-md text-black p-4 mt-8 mb-3 leading-none"
			>Register Now</button
		>

		<a
			on:click|preventDefault={info}
			href="https://www.servian.com/lookeratlightspeed"
			class="text-xs underline">Click here for more information</a
		>
	</div>
</main>
