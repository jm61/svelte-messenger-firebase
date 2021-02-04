<script>
    import {Collection} from 'sveltefire'
    import AppendMessage from './AppendMessage.svelte'
    import {tick} from 'svelte'
    export let user
    let chatsElem

    async function scrollToTheEnd() {
        await tick()
        chatsElem.scrollTo(0, chatsElem.scrollHeight)
    }
</script>
<Collection path={'/chat'} let:ref={chatsRef} let:data={messages} on:data={scrollToTheEnd}>
    <div class="box chat-box" bind:this={chatsElem}>
        {#each messages.sort((a,b)=> a.date - b.date) as {message,uid}}
            <div class="notification {uid === user.uid ? 'is-info is-sender': 'is-success is-receiver' } ">
                {message} 
            </div>
        {/each}
    </div>
    <AppendMessage {chatsRef} {user} />
</Collection>

<style>
    .chat-box {
        flex: 1;
        display: flex;
        flex-direction: column;
        overflow-y: auto;
    }
    .is-sender {
        text-align: left;
        margin-right: 7rem;
    }
    .is-receiver {
        text-align: right;
        margin-left: 7rem;
    }
</style>