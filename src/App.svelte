<script>
	import {FirebaseApp, User} from 'sveltefire'
	import firebase from 'firebase/app'
	import 'firebase/firestore'
	import 'firebase/auth'
	import AuthForm from './components/AuthForm.svelte'
	import Chats from './components/Chats.svelte'

	const firebaseConfig = {
    apiKey: "AIzaSyALPrn-h-uwvY1MLSFSWZgWV9UK_I95uDw",
    authDomain: "coderssvelte.firebaseapp.com",
    databaseURL: "https://coderssvelte.firebaseio.com",
    projectId: "coderssvelte",
    storageBucket: "coderssvelte.appspot.com",
    messagingSenderId: "311825050339",
    appId: "1:311825050339:web:61845c428e241292ab73d6"
  };
  firebase.initializeApp(firebaseConfig);


</script>

<main class="container section has-background-grey-light app">
	<h1 class="title has-text-info has-text-centered">Svelte Firebase Chat</h1>
	<FirebaseApp {firebase} >
		<User let:user let:auth>
			<Chats {user} />
			<mark class="has-text-centered">{user.email}</mark>
			<button class="button is-fullwidth has-background-success" on:click={()=> auth.signOut()}>Sign Out</button>
			<div slot="signed-out">
				<AuthForm {auth} />
			</div>
		</User>
	</FirebaseApp>
</main>

<style>
	.app {
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		max-height: 100vh;
	}
</style>

