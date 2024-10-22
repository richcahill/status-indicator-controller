<script>
	import '../app.css';
	import Nav from '$lib/components/Nav.svelte';
	import Login from '$lib/components/Login.svelte';
	import { FirebaseApp, SignedIn, SignedOut } from 'sveltefire';
	import { auth, firestore } from '$lib/firebase';
	import { checkEmail } from '$lib/index';

	let { children } = $props();

	$effect(() => {
		if (auth.currentUser) {
			console.log(auth.currentUser);
			if (!checkEmail(auth.currentUser.email)) {
				signOut(auth);
			}
		}
	});
</script>

<svelte:head>
	<title>Status Indicator Controller</title>
	<link
		rel="icon"
		href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22 fill=%22white%22>✴︎</text></svg>"
	/>
</svelte:head>

<FirebaseApp {auth} {firestore}>
	<SignedOut>
		<Login />
	</SignedOut>
	<SignedIn>
		<div class="flex flex-col min-h-screen">
			<Nav />
			<div class="flex-grow overflow-y-auto max-w-5xl w-full mx-auto p-2 flex flex-col">
				{@render children()}
			</div>
		</div>
	</SignedIn>
</FirebaseApp>
