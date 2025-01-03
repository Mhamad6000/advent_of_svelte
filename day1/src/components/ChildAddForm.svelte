<script lang="ts">
	let {
		children
	}: {
		children: { name: string; tally: number }[];
	} = $props();
	function handleSubmit(event: SubmitEvent & { currentTarget: EventTarget & HTMLFormElement }) {
		event.preventDefault();
		const data = new FormData(event.currentTarget);
		children.unshift({
			name: data.get('name') as string,
			tally: parseInt(data.get('tally') as string)
		});
	}
</script>

<form onsubmit={handleSubmit} method="post" class="mb-8 rounded-lg bg-white p-6 shadow-md">
	<div class="flex flex-wrap gap-4">
		<div class="min-w-[200px] flex-1">
			<label for="name" class="mb-1 block text-sm font-medium text-gray-700">Child's Name</label>
			<input
				id="name"
				name="name"
				required
				type="text"
				placeholder="Enter name"
				class="w-full rounded-md border border-gray-300 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-green-500"
			/>
		</div>
		<div class="w-32">
			<label for="tally" class="mb-1 block text-sm font-medium text-gray-700">Tally</label>
			<input
				id="tally"
				name="tally"
				required
				type="number"
				placeholder="Score"
				class="w-full rounded-md border border-gray-300 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-green-500"
			/>
		</div>
		<div class="flex w-full items-end sm:w-auto">
			<button
				type="submit"
				class="w-full rounded-md bg-green-600 px-4 py-2 text-white transition-colors hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-green-500 focus:ring-offset-2"
			>
				Add Child
			</button>
		</div>
	</div>
</form>
