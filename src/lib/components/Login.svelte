<script>
	import { Loader } from 'lucide-svelte';
	import { auth } from '$lib/firebase';
	import { SignedIn, SignedOut, Doc, Collection } from 'sveltefire';
	import { signInAnonymously, GoogleAuthProvider, signInWithPopup } from 'firebase/auth';
	const provider = new GoogleAuthProvider();
</script>

<div class="flex flex-col gap-2 h-screen justify-center items-center">
	<div class="flex flex-col gap-2 w-64 p-4 border rounded-md">
		<div class="flex justify-center pb-4">
			<Loader class="w-8 h-8" />
		</div>
		<button class="" on:click={() => signInWithPopup(auth, provider)}>Sign in with Google</button>
	</div>
</div>

<style>
	button {
		@apply bg-black text-white p-2 px-4 rounded-sm;
	}
</style>
