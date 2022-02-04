<script>
    export let rows = 5;
    export let grid = false;
    // import slot from "svelte"
</script>
<div class="row" style={grid ? `grid-template-columns: repeat(${rows}, 1fr); display: grid;` : `display: flex;`}>
    <slot></slot>
</div>

<style>
    .row {
        gap: 0.4rem;
        margin-bottom: 0.4rem;
    }
    /* .grid { */
        /* display: grid; */
    /* } */
    /* .f lex { */
        /* display: flex; */
        /* flex-grow: 1; */
    /* } */
</style>