<script lang="ts">
	import { page } from '$app/state';
	import { organizationStore } from '$lib/store/facilityStore';
	import * as m from "$msgs";
	import OpenGraph from '$lib/components/OpenGraph/OpenGraph.svelte';
	import { language } from '$lib/store/languageStore';
	import { capitalizeFirstLetter } from '$lib/helpers/stringHelpers';
	import type { PageData } from './$types';
	//import LDTag from '$lib/Schema/LDTag.svelte';
	import Directory from '$lib/components/Directory/CtxDirectory.svelte';
	export let data: PageData;
</script>

<!--LDTag schema={data.websiteSchema} /-->
<svelte:head>
	{#if data?.openGraph}
		<OpenGraph opengraph={data.openGraph} />
	{/if}

	<title>
		Annuaire - {capitalizeFirstLetter($organizationStore.formatted_name, $language)}
	</title>
</svelte:head>
<div>
	<!-- hero -->
	<header id="hero" class="bg-surface-100-800-token hero-gradient">
		<div class="section-container">
			<h2 class="h2">
				{m.ADDRESSBOOK_TITLE()}
			</h2>
		</div>
	</header>
	<div>
		{#key [page.url]}
		<Directory
		data={data?.cardinal}
		propCurrentOrg={true}
		displayCommune={false}
		displayCategory={true}
		avatar={true} />
		{/key}
	</div>
</div>

<style lang="postcss">
	.section-container {
		@apply w-full max-w-7xl mx-auto p-4 py-8 md:py-10;
	}
	/* Hero Gradient */
	/* prettier-ignore */
	.hero-gradient {
		background-image:
			radial-gradient(at 0% 0%, rgba(var(--color-secondary-500) / 0.33) 0px, transparent 50%),
			radial-gradient(at 98% 1%, rgba(var(--color-error-500) / 0.33) 0px, transparent 50%);
	}
</style>
