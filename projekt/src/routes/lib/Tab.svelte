<script>
	import { getContext } from 'svelte';
	import { TABS } from './Tabs.svelte';

	const tab = {};
	const { registerTab, selectTab, selectedTab } = getContext(TABS);

	registerTab(tab);
</script>

<button class:selected={$selectedTab === tab} on:click={() => selectTab(tab)}>
	<slot />
</button>

<style>
	button {
		background: none;
		border: none;
		border-bottom: 4px solid white;
		border-radius: 0;
		margin-right: 5rem;
		color: #ccc;
	}

	.selected {
		border-bottom: 2px solid teal;
		color: rgb(51, 51, 51);
	}
</style>
