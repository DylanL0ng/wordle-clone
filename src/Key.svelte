<script>
    import { createEventDispatcher, onMount } from "svelte/internal";
    import { RegisteredKeys } from "./stores/stores"
    
    const dispatch = createEventDispatcher()

    export let letter

    let pressedKey = false;

    let keyElement;
    onMount(() => {
        RegisteredKeys.update(n => [...n, { id: letter, el: keyElement }])
    })

    const clickKey = e => {
        dispatch("click-key", { which: letter.charCodeAt(0) })
        // window.dispatchEvent(new KeyboardEvent("keydown", { which: letter.charCodeAt(0) }))
        // console.log(letter)
    }
</script>

<div on:click={clickKey} bind:this={keyElement} class={`letter ${letter == 'ENT' || letter == "BCKSP" && "double-space"} ${pressedKey && "pressed"}`} >
    {#if letter == "\r"}
        {"ENTER"}
    {:else}
        {letter}
    {/if}
</div>


<style>
    div {
        cursor: pointer;
    }
    .letter {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-grow: 1;
        background: #333;
        border-radius: 0.2rem;
        padding-block: 1.25rem;
    }
    .empty-space {
        flex-grow: 0.5;
    }
    .double-space {
        flex-grow: 1.5;
    }
    .pressed {
        background-color: gray;
    }
</style>