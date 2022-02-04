<script>
    import { scale } from "svelte/transition"
</script>

<div transition:scale></div>

<style>
    div {
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 1.5rem;
        /* background: #333; */
        /* gap: 0; */
        border: 2px solid #444;
        aspect-ratio: 1;
    }
    /* .letter {
        flex-grow: 1;
        background: green;
    } */
</style>