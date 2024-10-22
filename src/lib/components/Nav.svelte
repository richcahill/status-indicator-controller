<script>
	import { Loader, LogOut } from 'lucide-svelte';
	import { userStore, FirebaseApp } from 'sveltefire';
	import { auth } from '$lib/firebase';
	import { signOut } from 'firebase/auth';
</script>

<nav class="w-full p-2 pb-0">
	<div
		class="grid grid-cols-3 justify-between items-center p-3 px-3 max-w-5xl mx-auto bg-gray-100 rounded-lg"
	>
		<div class="flex items-center gap-4">
			<a href="/">
				<Loader class="w-4 h-4" />
			</a>
		</div>
		<div class="flex items-center justify-center gap-4">
			<!-- <a href="/">Home</a>
				<a href="/about">About</a> -->
		</div>
		<div class="flex items-center justify-end gap-4">
			{#if auth}
				{auth?.currentUser?.email}
			{/if}
			<button on:click={() => signOut(auth)} class="hover:text-gray-500">
				<LogOut class="w-4 h-4" />
			</button>
		</div>
	</div>
</nav>
