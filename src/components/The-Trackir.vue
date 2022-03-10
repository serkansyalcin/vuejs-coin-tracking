
<template>
	<div class="tracir-body">
		<div class="refresh-and-add-btn">
			<button  class= "refresh">Refresh</button>
			<button @click= "clicked">Add Symbol</button>
		</div>
		<div>
		
		</div>
		<div><div v-if="isClicked" class="popup"><PopUp :coinData="coinData" @addclick="addCoinInfo" @close="closepop"/>
		</div></div>
		<div class="addedCoins" ref="addedCoins">
		
				<AddedCoins :addedCoins="addedCoins" @removeCoin="removeCoin"/>
		
		</div>
		
	</div>
</template>

<script>
	import axios from 'axios';
	import PopUp from './The-Pop-up.vue';
	import AddedCoins from './The-Added-Coins.vue'

	export default {
		name: 'The-Trackir',

		components: {
		PopUp,
		AddedCoins,
	},
	async mounted(){
		await axios.get('https://api2.binance.com/api/v3/ticker/24hr')
		.then(res => {
			this.coinData = res.data.map( item => item)
			console.log(this.coinData)
		})
		.catch(err => {
			console.log(err)
		})
	},
		data () {
			return {
				test: 'First Test',
				isClicked:  false,
				coinData: '',
				addedCoins: [],
			}
		},
		methods: {
			clicked () {
				this.isClicked = !this.isClicked;
				
			},
			closepop () {
				this.isClicked = !this.isClicked;
			},
			addCoinInfo (symbol, lastPrice, weightedAvgPrice) {
				this.addedCoins.push({
					symbol: symbol,
					lastPrice: lastPrice,
					weightedAvgPrice: weightedAvgPrice
				})
				console.log(this.addedCoins)
				
			}, 
			addToDOM(){

			},
			removeCoin(symbol){
				console.log('removedcoin')
				const index = this.addedCoins.findIndex(coin => coin.symbol === symbol)
				this.addedCoins.splice(index, 1)
			}
			
		}
	
	}
</script>

<style scoped>
	.tracir-body {
		display: flex;
		justify-content: center;
		position: absolute;
		top: 10%;
		left: 30%;
		width: 660px;
		height: 600px;
		background-color: #ffff;
		border-radius: 5px;
	}
	.refresh{
		margin-right: 20px;
	}
	.refresh-and-add-btn {
		display: flex;
		align-items: end;
		justify-content: end;
		width: 550px;
		height: 100px;
		border-bottom: 2px solid black;
		padding-bottom: 15px;
		
	}

	.refresh-and-add-btn button {
		width: 121px;
		height: 43px;
		border:  1px solid #000000;
		border-radius: 5px;
		font-weight: 400;
		font-size: 12px;
		font-family: Roboto;
		background-color: transparent;
		cursor: pointer;
	}
	.popup{
		height: 100vh;
		margin-top: auto;
		
		
		
	}
	.addedCoins{
		position: absolute;
		top: 20%;
		right: 10%;
		margin-right: -40px;
		width: 90%;
		z-index: 1;
	}
	
	
	
</style>