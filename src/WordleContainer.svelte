<script>
    import { onMount } from "svelte/internal";

    import LetterBox from "./LetterBox.svelte"
    import Row from "./Row.svelte"
    import {scale} from "svelte/transition"
    
    export let challenge_width = 30;
    
    let onLoad = false

    onMount(() => {
        setTimeout(() => {
            onLoad = true
        }, 150);

        // console.log(challenge_width)
    })
</script>

<div class="word-container" style={`width: ${challenge_width}%;`}>
    {#if onLoad}
        {#each Array(6) as _, x } <!-- Row -->
            <Row grid=true>
                {#each Array(5) as _, i } <!-- Columns -->
                    <LetterBox />
                {/each}
            </Row>
        {/each}
    {/if}
</div>

<style>
    .word-container {
        display: grid;
        grid-template-rows: repeat(6, 1fr);
        /* gap: 0.5rem; */
        margin-inline: auto;
		width: 70%;
		padding: 1.5rem;
        max-width: 20rem;
    }
    /* .row {
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        gap: 0.5rem;
    } 
    */
</style>