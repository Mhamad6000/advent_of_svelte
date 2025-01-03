<script lang="ts">
	import type { PageData } from './$types';
	import Child from '@/components/Child.svelte';
	import ChildAddForm from '@/components/ChildAddForm.svelte';
	let { data }: { data: PageData } = $props();
	let children = $state(data?.children);
	let niceChildren = $derived.by(() => {
		return children?.filter((child: { name: string; tally: number }) => {
			return child?.tally >= 0;
		});
	});
	let naughtyChildren = $derived.by(() => {
		return children?.filter((child: { name: string; tally: number }) => {
			return child?.tally < 0;
		});
	});
</script>

<div class="container">
	<div class="mx-auto max-w-7xl">
		<h1 class="mb-5 text-center text-3xl font-bold text-gray-800">Santa's List Manager</h1>
		<ChildAddForm {children} />
		<div class="grid gap-5 sm:grid-cols-2">
			<div class="rounded-lg bg-white p-6 shadow-md">
				<h2 class="mb-4 flex items-center text-2xl font-semibold text-green-600">
					<svg class="mr-2 h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M5 13l4 4L19 7"
						/>
					</svg>
					Nice
				</h2>
				<div class="flex flex-col gap-3">
					{#each niceChildren as child, i (i)}
						<Child
							childData={{
								name: child?.name,
								tally: child?.tally,
								type: 'nice'
							}}
						/>
					{/each}
				</div>
			</div>
			<div class="rounded-lg bg-white p-6 shadow-md">
				<h2 class="mb-4 flex items-center text-2xl font-semibold text-red-600">
					<svg class="mr-2 h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M6 18L18 6M6 6l12 12"
						/>
					</svg>
					Noughty
				</h2>
				<div class="flex flex-col gap-3">
					{#each naughtyChildren as child, i (i)}
						<Child
							childData={{
								name: child?.name,
								tally: child?.tally,
								type: 'naughty'
							}}
						/>
					{/each}
				</div>
			</div>
		</div>
	</div>
</div>
