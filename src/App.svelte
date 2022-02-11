<script>
	const cardImages = [
		{ src: "/public/img/helmet-1.png" },
		{ src: "/public/img/potion-1.png" },
		{ src: "/public/img/ring-1.png" },
		{ src: "/public/img/scroll-1.png" },
		{ src: "/public/img/shield-1.png" },
		{ src: "/public/img/sword-1.png" },
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
	const shuffleCards = () => {
		const shuffledCards = shuffle([...cardImages, ...cardImages]).map(
			(card) => ({ ...card, id: Math.random() })
		);

		turns = 0;
	};
</script>

<main>
	<h1>Magic Match</h1>
	<button on:click={shuffleCards}>New Game</button>
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
</style>
