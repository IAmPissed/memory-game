<script>
	export let card;
	export let handleChoice;
	export let flipped;
	export let disabled;

	const handleClick = () => {
		if (!disabled) {
			handleChoice(card);
		}
	};
</script>

<div class="card">
	<div class={flipped ? "flipped" : ""}>
		<img src={card.src} alt="card front" class="front" />
		<img
			src="/img/cover.png"
			alt="card back"
			class="back"
			on:click={handleClick}
		/>
	</div>
</div>

<style>
	.card {
		position: relative;
	}
	.card img {
		width: 100%;
		display: block;
		border: 0.2rem solid white;
		border-radius: 0.6rem;
	}
	.card .front {
		position: absolute;
		transform: rotateY(90deg);
		transition: all ease-in 0.2s;
	}
	.flipped .front {
		transform: rotateY(0deg);
		transition-delay: 0.2s;
	}
	.card .back {
		transition: all ease-in 0.2s;
		transition-delay: 0.2s;
	}
	.flipped .back {
		transform: rotateY(90deg);
		transition-delay: 0s;
	}
</style>
