<script>
    import { createEventDispatcher, onMount } from "svelte/internal";

    const dispatch = createEventDispatcher()

    let header_bottom = null
    onMount(() => {
        setTimeout(() => {
            dispatch("header-element", header_bottom)
        }, 150);
    })
</script>

<header>
	<h1>
		Wordle
	</h1>
</header>
<hr	bind:this={header_bottom} />

<style>
    header {
		/* padding: 0.2rem; */
		display: flex;
		justify-content: center;
		align-content: center;
	}
	header h1 {
		text-transform: uppercase;
		letter-spacing: 0.2rem;
		font-size: 2.5rem;
		margin: 0;
	}
	hr {
		margin: 0;
		border-width: 2px;
		border-color: #333;
	}
</style>