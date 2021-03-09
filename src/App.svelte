<script lang="ts">
	export let name: string;
	let coin = 0;
	let clickpower = 1;

	let upgrades1 = 0

	let Cost_upgrade1 = 10;
	function _CoinClicked(){
		coin += clickpower
	}
	function _Buyable(cost){
		if (coin >= cost){
			return true;
		}
	}
	function _Upgrade1(){
		if(_Buyable(Cost_upgrade1)){
			clickpower += 1
			upgrades1 += 1
			coin -= Cost_upgrade1
			Cost_upgrade1 = 10 * Math.round(Math.pow((upgrades1 * 1.5), 2)) + 10
		}
	}
</script>

<svelte:head>
	<title>Svelte-Clicker</title>
</svelte:head>

<main>
	<div>
		<h1>Hello {name}!</h1>
		<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
	</div>
	<div>
		<p>ClickPower: {clickpower}</p>
		<button on:click="{_CoinClicked}">Get Coin</button>
	</div>
	<div>
		<p>Coins = {coin}</p>
	</div>
	<div>
		<button on:click="{_Upgrade1}">+1</button>
		<p>costs: {Cost_upgrade1} coins</p>
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>