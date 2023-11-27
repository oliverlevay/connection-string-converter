<script lang="ts">
	import CopyMe from './CopyMe.svelte';

	let connectionString = 'postgres://postgres:postgres@localhost:5432/test';
	let isValid = true;
	let connectionProperties = {
		user: '',
		pass: '',
		host: '',
		port: '',
		database: ''
	};
	$: (() => {
		try {
			const parts = connectionString.split('@');
			const userPass = parts[0].split('://')[1];
			const hostPort = parts[1].split('/')[0];
			const database = parts[1].split('/')[1];
			const user = userPass.split(':')[0];
			const pass = userPass.split(':')[1];
			const host = hostPort.split(':')[0];
			const port = hostPort.split(':')[1];
			if (!user || !pass || !host || !port || !database)
				throw new Error('Invalid connection string');
			connectionProperties = {
				user,
				pass,
				host,
				port,
				database
			};
			isValid = true;
		} catch {
			isValid = false;
		}
	})();
</script>

<title> Connection string converter </title>

<div class="gap-4 flex flex-col">
	<h1 class="text-3xl">Connection string converter</h1>
	<p class="text-gray-500">
		Convert a connection string to individual properties, paste a connection string to get started.
	</p>

	<input
		type="text"
		class=" rounded-md p-2 w-80"
		placeholder="Connection string"
		bind:value={connectionString}
	/>

	{#if !isValid}
		<p class="text-red-500">Invalid connection string</p>
	{:else}
		<p class="">Copy to your hearts content!</p>
	{/if}

	<CopyMe label="Host" value={connectionProperties.host} />
	<CopyMe label="User" value={connectionProperties.user} />
	<CopyMe label="Password" value={connectionProperties.pass} />
	<CopyMe label="Port" value={connectionProperties.port} />
	<CopyMe label="Database" value={connectionProperties.database} />
</div>
