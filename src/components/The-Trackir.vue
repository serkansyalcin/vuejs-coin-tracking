
<template>
	<div class="tracir-body">
		<div class="refresh-and-add-btn">
			<button @click= "clicked">Add Symbol</button>
		</div>
		<div>
		
		</div>
		<div><div v-if="isClicked" class="popup"><PopUp :coinData="coinData" @addclick="addCoinInfo" @close="closepop"/>
		</div></div>
		<div class="addedCoins" ref="addedCoins">
			<div v-for="(addedCoin, index) in addedCoins" :key="index" class="addedcoins1">
				{{addedCoin.symbol}} - {{addedCoin.lastPrice}} - {{addedCoin.weightedAvgPrice}} <span><button class="remove">remove</button></span>
			</div>
		</div>
		
	</div>
</template>

<script>
	import axios from 'axios';
	import PopUp from './The-Pop-up.vue';

	export default {
		name: 'The-Trackir',

		components: {
		PopUp,
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
		top: 30%;
		right: 10%;
		margin-right: -40px;
		width: 90%;
		overflow-y: scroll;
		z-index: 1;
	}
	.addedcoins1{
		display: flex;
		justify-content: space-between;
		padding: 5px;
		border: black solid 1px !important;
		border-radius: 5px;
		margin-top: 10px;
		
	}
	.remove{
		background-color: #F8B1AC;
		border: none;
		border-radius: 5px;
		padding: 5px;
		margin-left: 10px;
		cursor: pointer;
	}
	
</style>