<script>
    export let auth
    let mode = "signIn"
    let email, password = ""
    $:field = "Enter Chat"

    async function handleSubmit() {
        if(mode === 'signIn') {
            await auth.signInWithEmailAndPassword(email, password)        
    } else {
        await auth.createUserWithEmailAndPassword(email, password)
    } email = ''; password = '';
}

</script>
<h1 class="title has-text-info has-text-centered">Svelte Firebase Chat</h1>
<h2 class="is-size-3"> {mode === 'signIn' ? 'Sign In': 'Sign Up'} </h2>
<form on:submit|preventDefault={handleSubmit}>
    <div class="field">
        <label for="email" class="label">Email
            <input type="email" class="input" bind:value={email} placeholder="enter your email..." autocomplete="off" required>
        </label>
    </div>
    <div class="field">
        <label for="password" class="label">Password
            <input type="password" class="input" bind:value={password} placeholder="enter your password..." required>
        </label>
        <div class="field">
            <input type="submit" class="button is-fullwidth" value={field}>
        </div>
    </div>
</form>
<hr>
{#if mode === 'signIn'}
    <p>if you need an account please: <span class="has-text-link link" on:click={()=> (mode = 'signUp') (field = 'Register')}>Sign Up</span></p>
{:else}
<p> if you have an account please: <span class="has-text-link link" on:click={()=> (mode = 'signIn') (field = 'Enter Chat')}>Sign In</span></p>
{/if}

<style>
    .link { cursor: pointer;}
</style>