<script>
	import 'focus-visible';
	import BouncyBtn from './BouncyBtn.svelte'
	let gCount = 0, bCount = 0, mCount = 0
</script>

<main>
	<h1>Svelte Bouncy, Variable-Font Buttons</h1>
	<div>
		<span>
			<p>{gCount}</p>
			<BouncyBtn amount={20} duration={600} gluten on:click={()=> gCount += 1}>CLICK ME</BouncyBtn>
			<a href="https://fontesk.com/gluten-typeface/">Gluten</a> by Tyler Fink
		</span>
		<span>
			<p>{bCount}</p>
			<BouncyBtn amount={10} duration={1500} barlow on:click={()=> bCount += 1}>CLICK ME</BouncyBtn>
			<a href="https://github.com/jpt/barlow">Barlow</a> by Jeremy Tribby
		</span>
		<span>
			<p>{mCount}</p>
			<BouncyBtn amount={40} duration={800} mutator on:click={()=> mCount += 1}>CLICK ME</BouncyBtn>
			<a href="https://fontesk.com/mutator-sans-font/">Mutator Sans</a> by Erik van Blokland
		</span>
	</div>
</main>


<style>
	div {
		display: grid;
		width: 100%;
		grid-gap: 1rem;
		justify-content: center;
		margin-top: 50px;
	}
	main {
		text-align: center;
	}
	span {
		display: flex;
		flex-direction: column;
		background: #f2f2f2;
		border-radius: 1.5rem;
		padding: 2rem;
		align-items: center;
		position: relative
	}
	p {
		position: absolute;
		bottom: 5px;
		right: 5px;
		background-color: #e3e1e1;
		color: #999;
		padding: .5rem;
		font-weight: bold;
		border-radius: 999px;
		height: 30px;
		width: 30px;
		display: flex;
		align-items: center;
		justify-content: center;
		margin: 0
	}
</style>