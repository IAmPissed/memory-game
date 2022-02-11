<script>
	export let card;
</script>

<div class="card">
	<div>
		<img src={card.src} alt="card front" class="front" />
		<img src="/img/cover.png" alt="card back" class="back" />
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
</style>
