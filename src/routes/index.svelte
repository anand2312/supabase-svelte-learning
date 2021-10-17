<script>
	import { supabase } from './_client.js';

	let user = supabase.auth.user();
</script>

<svelte:head>
	<title>Maybe a Chat App</title>
</svelte:head>

<section>
	<h1>Maybe a Chat App</h1>

	{#if user}
		<h2>Hi {user.email}!</h2>
		<center><a href="/rooms">Here are your chatrooms!</a></center>
		<br>
		<center><a href="/newroom">Click here to create a new room!</a></center>
	{:else}
		<p>Latest bleeding edge chatroom moment.</p>
	{/if}
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	h1 {
		width: 100%;
	}
</style>
