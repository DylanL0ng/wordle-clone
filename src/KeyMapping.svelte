<script>
    import Row from "./Row.svelte"
    import Key from "./Key.svelte"
    import { RegisteredKeys } from "./stores/stores"
    import { createEventDispatcher, onMount } from "svelte"


    const dispatch = createEventDispatcher()

    export let keyboard_element = null

    let keymapping = [
        [ "Q", "W", "E", "R", "T", "Y", "U", "I", "O", "P" ],
        [ "", "A", "S", "D", "F", "G", "H", "J", "K", "L", "" ],
        [ "\r", "Z", "X", "C", "V", "B", "N", "M", "BCKSP" ],
    ]


    let keys = [];

    const checkKeyPress = (e) => {
        const letter = String.fromCharCode(e.which).toUpperCase()

        keys = $RegisteredKeys;
        if (!keys.some(e => e.id === letter)) return;
        
        keys.forEach(e => {
            if (e.id === letter) {
                if (e.pressed) return;
                e.el.classList.add("pressed")
                e.pressed = true;
                return
            }
        })

        RegisteredKeys.update(n => keys)
    }

    onMount(() => {
        setTimeout(() => {
            dispatch("keyboard-element", keyboard_element)
        }, 150);
    })
</script>

<div class="keyboard" bind:this={keyboard_element}>
    {#each keymapping as row, i}
        <Row>
            {#each row as letter, x}
                {#if letter == ""}
                    <div class="empty-space"></div>
                {:else}
                    <Key on:click-key={(e) => checkKeyPress(e.detail)} letter={letter} />
                {/if}
            {/each}
        </Row>
    {/each}
</div>

<svelte:body on:keypress={checkKeyPress} />

<style>
    .keyboard {
        margin-inline: 0.5rem;
        position: absolute;
        bottom: 0;
        right: 0;
        left: 0;
    }
</style>