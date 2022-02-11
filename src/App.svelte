<script>
	import SingleCard from "./components/SingleCard.svelte";

	const cardImages = [
		{ src: "/img/helmet-1.png" },
		{ src: "/img/potion-1.png" },
		{ src: "/img/ring-1.png" },
		{ src: "/img/scroll-1.png" },
		{ src: "/img/shield-1.png" },
		{ src: "/img/sword-1.png" },
	];
	$: turns = 0;

	function shuffle(arr) {
		let i = arr.length,
			randomIndex,
			temp,
			newArr = arr;
		while (--i > 0) {
			randomIndex = Math.floor(Math.random() * (i + 1));
			temp = newArr[randomIndex];
			newArr[randomIndex] = newArr[i];
			newArr[i] = temp;
		}
		return newArr;
	}

	// Shuffle Cards
	let cards = [];
	const shuffleCards = () => {
		const shuffledCards = shuffle([...cardImages, ...cardImages]).map(
			(card) => ({ ...card, id: Math.random() })
		);
		turns = 0;
		cards = shuffledCards;
	};
	shuffleCards();
</script>

<main>
	<div class="container">
		<h1>Magic Match</h1>
		<button on:click={shuffleCards}>New Game</button>
		<div class="card-grid">
			{#each cards as card (card.id)}
				<SingleCard {card} />
			{/each}
		</div>
	</div>
</main>

<style>
	h1 {
		margin-bottom: 1rem;
	}
	button {
		background: none;
		border: 0.2rem solid white;
		padding: 0.6em 1.2em;
		border-radius: 0.4em;
		font-weight: 500;
		cursor: pointer;
		color: white;
		transition: all 200ms linear;
	}
	button:hover {
		background: hsl(340, 55%, 49%);
		color: white;
	}
	.card-grid {
		margin-top: 4rem;
		display: grid;
		grid-template-columns: repeat(4, 10rem);
		gap: 2rem;
		justify-content: center;
	}
</style>
