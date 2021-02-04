<script>
    export let chatsRef
    export let user
    let message = ""

    async function appendMessage() {
        if(!message) return
        await chatsRef.add({message, uid: user.uid, date: Date.now()})
        message = ""
    }
</script>
<form on:submit|preventDefault={appendMessage}>
    <div class="field has-addons box">
        <div class="control is-expanded">
            <input type="text" class="input" bind:value={message} placeholder="type some message..." required>
        </div>
        <div class="control">
            <input type="submit" value="Send" class="button is-info">
        </div>
    </div>
</form>