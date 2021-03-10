<script lang="ts">
	
	var timer = setInterval(_GiveCPS, 100)

	window.Give = Give;
	

	let values = {
		coins: 0,
		coinsPS: 0,
		clickpower: 1,
	};


	let upgrades1 = 0
	let upgrades2 = 0

	

	let Cost_upgrade1 = 10;
	let Cost_upgrade2 = 50;

	let psupgrades1 = 0

	let Cost_psupgrade1 = 1;

	function _GiveCPS(){
		values.coins += (values.coinsPS/10)
	}

	function _CoinClicked(){
		values.coins += values.clickpower
	}

	export function Give(type: string, amount: number){
		values[type] += amount
	}

	function _Buyable(cost){
		if (values.coins >= cost){
			return true;
		}
	}
	function _Upgrade1(){
		if(_Buyable(Cost_upgrade1)){
			values.clickpower += 1
			upgrades1 += 1
			values.coins -= Cost_upgrade1
			Cost_upgrade1 = Math.pow((upgrades1), 2) * upgrades1 + 10
		}
	}
	function _Upgrade2(){
		if(_Buyable(Cost_upgrade2)){
			values.clickpower += 2
			upgrades2 += 1
			values.coins -= Cost_upgrade2
			Cost_upgrade2 = 10 * Math.pow((upgrades2 * 2), 2) * upgrades2 + 50
		}
	}
	function _PsUpgrade1(){
		if(_Buyable(Cost_psupgrade1)){
			values.coinsPS += 1
			psupgrades1 += 1
			values.coins -= Cost_psupgrade1
			Cost_psupgrade1 = 10 * Math.pow((psupgrades1 * 2), 2) * psupgrades1 + 1
		}
	}
</script>

<svelte:head>
	<title>Svelte-Clicker</title>
</svelte:head>

<main>
	<div class="grid-container-Main">
		<div>
			<p>ClickPower: {values.clickpower}</p>
			<p>Coins/s: {values.coinsPS}</p>
			<button on:click="{_CoinClicked}">Get Coin</button>
		</div>
		<p>Coins = {Math.round(values.coins)}</p>
	</div>
	
	<div class="grid-container-Upgrades">
		<div class="upgradeButtons">
			<button on:click="{_Upgrade1}">+1 Click</button>
			<p class="upgradeCost">costs: {Cost_upgrade1} coins</p>
		</div>
		<div class="upgradeButtons">
			<button on:click="{_Upgrade2}">+2 Click</button>
			<p class="upgradeCost">costs: {Cost_upgrade2} coins</p>
		</div>
		<div class="upgradeButtons">
			<button on:click="{_PsUpgrade1}">+1 cPS</button>
			<p class="upgradeCost">costs: {Cost_psupgrade1} coins</p>
		</div>
	</div>
	
	<footer>
		<p>built using <a href="https://svelte.dev">Svelte</a> and <a href="https://www.typescriptlang.org/">typescript</a></p>
	</footer>
</main>


<style>
	main {
		text-align: center;
		max-width: 240px;
		min-height: 100vh;
		margin: 0 auto;
		height: 90%;
		display: grid;
		grid-template-columns: [ClickAreaStart]3fr [ClickAreaEnd UpgradeAreaStart] 1fr [UpgradeAreaEnd];
		grid-template-rows: [GameAreaStart] 9fr [GameAreaEnd FooterStart] 1fr [FooterEnd] ;
	}

	p {
		margin: inherit;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

	.grid-container-Main{
		grid-column-start: ClickAreaStart;
		grid-column-end: ClickAreaEnd;
		grid-row-start: GameAreaStart;
		grid-row-end: GameAreaEnd;
	}

	.grid-container-Upgrades{
		grid-column-start: UpgradeAreaStart;
		grid-column-end: UpgradeAreaEnd;
		grid-row-start: GameAreaStart;
		grid-row-end: GameAreaEnd;
		
	}

	.upgradeCost{
		margin: 0px;
	}

	.upgradeButtons {
		margin: 5px;
		background-color: beige;
	}

	footer{
		grid-column-start:ClickAreaStart;
		grid-column-end:UpgradeAreaEnd;
		grid-row-start: FooterStart;
		grid-row-end: FooterEnd;
		background-color: darkslategray;
		color:floralwhite;
	}
</style>