<script>
	import SingleCard from "./components/SingleCard.svelte";

	let disabled = false;
	$: turns = 0;
	let choiceOne = null;
	let choiceTwo = null;

	const cardImages = [
		{ src: "/img/helmet-1.png", matched: false },
		{ src: "/img/potion-1.png", matched: false },
		{ src: "/img/ring-1.png", matched: false },
		{ src: "/img/scroll-1.png", matched: false },
		{ src: "/img/shield-1.png", matched: false },
		{ src: "/img/sword-1.png", matched: false },
	];

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

	const resetTurn = () => {
		choiceOne = null;
		choiceTwo = null;
		turns = turns + 1;
		disabled = false;
	};

	// Shuffle Cards
	let cards = [];
	const shuffleCards = () => {
		const shuffledCards = shuffle([...cardImages, ...cardImages]).map(
			(card) => ({ ...card, id: Math.random() })
		);
		turns = 0;
		cards = shuffledCards;
		choiceOne = null;
		choiceTwo = null;
	};
	shuffleCards();

	const handleChoice = (card) => {
		choiceOne ? (choiceTwo = card) : (choiceOne = card);
		if (choiceOne && choiceTwo) {
			disabled = true;
			if (choiceOne.src === choiceTwo.src) {
				cards = cards.map((card) => {
					if (card.src === choiceOne.src) {
						return { ...card, matched: true };
					} else {
						return card;
					}
				});
				resetTurn();
			} else {
				setTimeout(() => resetTurn(), 1500);
			}
		}
	};
</script>

<main>
	<div class="container">
		<h1>Magic Match</h1>
		<button on:click={shuffleCards}>New Game</button>
		<div class="card-grid">
			{#each cards as card (card.id)}
				<SingleCard
					{card}
					{handleChoice}
					flipped={card === choiceOne || card === choiceTwo || card.matched}
					{disabled}
				/>
			{/each}
		</div>
		<p>Turns: {turns}</p>
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
		margin-bottom: 2rem;
		display: grid;
		grid-template-columns: repeat(4, 10rem);
		gap: 2rem;
		justify-content: center;
	}
	p {
		font-size: 1.6rem;
	}
</style>
