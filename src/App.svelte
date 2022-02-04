<script>
	import WordleContainer from "./WordleContainer.svelte";
	import Header from "./Header.svelte"
	import KeyMapping from "./KeyMapping.svelte";
	import { onMount } from "svelte/internal";
	import { RandomWord } from "./stores/stores"

	let word_list = []

	let keyboard_element = null
	let header_element = null

	$: challenge_width = 40;

	onMount(async () => {
		await fetch("https://raw.githubusercontent.com/charlesreid1/five-letter-words/master/sgb-words.txt")
		.then(res => res.text())
		.then(res => {
			word_list = res.split('\n')
		})

		console.log(challenge_width)

		// console.log(Math.floor(Math.random() * word_list.length))

		let random_word = word_list[Math.floor(Math.random() * word_list.length)]

		// console.log(random_word)
		RandomWord.set(random_word.toUpperCase());

		setTimeout(() => {
			setChallengeWidth()
		}, 150);
		console.log($RandomWord)
	})

	const setKeyboard = ({ detail }) => {
		keyboard_element = detail
	}
	const setHeader = ({ detail }) => {
		header_element = detail
	}

	const setChallengeWidth = () => {
		const top = header_element.getBoundingClientRect().top;
		const bottom = keyboard_element.getBoundingClientRect().top;

		challenge_width = ((bottom - top) / 700)* 100
	}

	let old_height = undefined
	const handleResize = (e) => {
		if (old_height === window.innerHeight) return;
		old_height = window.innerHeight
		console.log('test')
		setChallengeWidth()
	}
</script>

<div on:resize={handleResize} class="flex-wrapper">
	<Header on:header-element={setHeader} />
	<WordleContainer challenge_width={challenge_width} />
	<KeyMapping on:keyboard-element={setKeyboard} />
</div>

<svelte:window on:resize={handleResize} />

<style>
	.flex-wrapper {
		height: 100vh;
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		max-width: 500px;
		margin-inline: auto;
		position: relative;
	}
</style>