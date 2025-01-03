<script lang="ts">
	import { fade } from 'svelte/transition';
	let {
		childData
	}: {
		childData: {
			name: string;
			tally: number;
			type: 'nice' | 'naughty';
		};
	} = $props();
</script>

<div
	transition:fade|local
	class="flex items-center justify-between p-3 {childData?.type === 'nice'
		? 'bg-green-50'
		: 'bg-red-50'} rounded-md"
>
	<div class="font-medium text-gray-800">{childData?.name}</div>
	<div
		class="px-3 py-1 {childData?.type === 'nice'
			? 'bg-green-100 text-green-800'
			: 'bg-red-100 text-red-800'} rounded-full text-sm"
	>
		{childData?.type === 'nice' ? '+' : ''}{childData?.tally}
	</div>
</div>
