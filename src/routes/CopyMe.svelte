<script lang="ts">
	export let label = '';
	export let value = '';
	function copy() {
		navigator.clipboard.writeText(value);
	}
</script>

<label aria-label="ge" class="text-gray-500 flex flex-col gap-2"
	>{label}
	<div class="flex flex-row gap-2">
		<input
			type="text"
			class="rounded-md p-2 w-80"
			placeholder="copy me later"
			bind:value
			disabled
		/>
		<button
			class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded w-80"
			on:click={copy}
		>
			Copy
		</button>
	</div>
</label>
