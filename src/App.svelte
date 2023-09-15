<script lang="ts">
	import { onMount, type ComponentType } from 'svelte';
	import Counter from './Counter.svelte';
  import TailwindCss from './TailwindCSS.svelte';
	import IconBackspaceFilled from '@tabler/icons-svelte/dist/svelte/icons/IconBackspaceFilled.svelte';


	let component: ComponentType;
	component = Counter;
	let counters: { component: ComponentType; count: number }[] = [];
	let inputVal: string[] = [];
	let totalCount: number;

	onMount(() => {
		addCounter(0);
	});

	function addCounter(initialCount: number) {
		const current = [...counters];
		current.push({ component, count: initialCount });
		counters = current;
		inputVal.push('');
	}

	function deleteCounter(i: number) {
		const current = [...counters];
		const deleted = current.splice(i, 1)[0];
		counters = current;
		if (deleted) {
			totalCount -= deleted.count;
			inputVal.splice(i, 1);
			inputVal = [...inputVal];
		}
	}

	$: {
		totalCount = counters.reduce((sum, { count }) => sum + count, 0);
	}
</script>

<TailwindCss />
<div class="text-center h-screen">
	<h1 class="py-4 text-5xl">Multiple Counter</h1>
	<div class="grid grid-cols-1 gap-2">
		{#each counters as { component, count }, i}
			<div class="flex justify-center">
				<Counter bind:count bind:input={inputVal[i]} />
				<button on:click={() => deleteCounter(i)} class="ml-2"><IconBackspaceFilled /></button>
			</div>
		{/each}
	</div>
	<button on:click={() => addCounter(0)} class="rounded my-4 px-2 w-1/4 bg-amber-100">Add Counter</button>
	<p class="font-bold">Total: {totalCount}</p>
	<p class="font-bold">Title: {inputVal}</p>
</div>