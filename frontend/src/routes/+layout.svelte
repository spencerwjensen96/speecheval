<script lang="ts">
    import "../app.pcss";
    import { onMount } from "svelte";
    import { authStore } from "../stores/authStore.js";
    import { auth } from "../lib/firebase/firebase.app";
    
    onMount(() => {
		const unsubscribe = auth.onAuthStateChanged((user) => {
			console.log(user);
			authStore.update((curr) => {
				return { ...curr, isLoading: false, currentUser: user };
			});

			// if (
			// 	!$authStore?.currentUser &&
			// 	!$authStore.isLoading &&
			// 	window.location.pathname !== '/login'
			// ) {
			// 	window.location.href = '/app';
			// }
		});
		return unsubscribe;
	});
</script>

<slot></slot>