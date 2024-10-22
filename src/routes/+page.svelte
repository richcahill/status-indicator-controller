<script>
	import { docStore } from 'sveltefire';
	import { firestore } from '$lib/firebase';
	import { setDoc, doc } from 'firebase/firestore';

	const text = docStore(firestore, 'status/text');

	let inputText = '';

	async function updateDocument() {
		const docRef = doc(firestore, 'status/text');
		try {
			await setDoc(docRef, { input: inputText });
			inputText = ''; // Clear input field after sending
		} catch (error) {
			console.error('Error updating document:', error);
		}
	}
</script>

<div class="flex flex-col gap-4 flex-grow bg-gray-100 rounded-lg p-4 items-center justify-center">
	<div class="flex gap-2 w-64 flex-col items-stretch p-2 border border-gray-200 rounded-sm">
		<input type="text" bind:value={inputText} placeholder="Enter your message" />
		<button on:click={updateDocument}>Send</button>
	</div>
	<div class="flex gap-2 w-64 flex-col items-center font-mono bg-black text-white p-4 rounded-sm">
		<h1>{$text?.input}</h1>
	</div>
</div>

<style>
	input {
		@apply p-2 rounded-sm border border-gray-300 text-center caret-pink-500 selection:bg-pink-500 selection:text-white text-pink-500;
	}

	input::placeholder {
		@apply text-gray-300;
	}

	input:focus {
		@apply ring-pink-500 border-pink-500;
	}

	button {
		@apply bg-pink-500 text-white p-2 px-4 rounded-sm;
	}
</style>
