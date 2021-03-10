<script lang="ts">
	let coin = 0;
	let clickpower = 1;
	let CoinPS = 0;
	
	var timer = setInterval(_GiveCPS, 1000)

	let upgrades1 = 0
	let upgrades2 = 0

	let Cost_upgrade1 = 10;
	let Cost_upgrade2 = 50;

	let psupgrades1 = 0

	let Cost_psupgrade1 = 100;

	function _GiveCPS(){
		coin += CoinPS
	}

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
			Cost_upgrade1 = Math.round(Math.pow((upgrades1), 2) * upgrades1) + 10
		}
	}
	function _Upgrade2(){
		if(_Buyable(Cost_upgrade2)){
			clickpower += 2
			upgrades2 += 1
			coin -= Cost_upgrade2
			Cost_upgrade2 = 10 * Math.round(Math.pow((upgrades2 * 2), 2) * upgrades2) + 50
		}
	}
	function _PsUpgrade1(){
		if(_Buyable(Cost_psupgrade1)){
			CoinPS += 1
			psupgrades1 += 1
			coin -= Cost_psupgrade1
			Cost_psupgrade1 = 10 * Math.round(Math.pow((psupgrades1 * 2), 2) * psupgrades1) + 100
		}
	}
</script>

<svelte:head>
	<title>Svelte-Clicker</title>
</svelte:head>

<main>
	<div class="grid-container-Main">
		<div>
			<p>ClickPower: {clickpower}</p>
			<p>Coins/s: {CoinPS}</p>
			<button on:click="{_CoinClicked}">Get Coin</button>
		</div>
		<p>Coins = {coin}</p>
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