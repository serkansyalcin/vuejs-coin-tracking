<template>
	<div class= "coins-container">
		<div class= "search"><span><input type="text" placeholder="search"></span><span @click="$emit('close')" style="cursor: pointer">X close</span></div>
		<!-- <div>{{selected}}</div> -->
		<div v-for="(coin,index) in coinData" :key="index" class="select-coin"> 
			{{coin.symbol}} - {{coin.lastPrice}} 
			<button class="button-add" @click="$emit('addclick', coin.symbol, coin.lastPrice, coin.weightedAvgPrice), disabled1()" :disabled="!disable">add</button>
		</div>
	
	</div>
</template>

<script>
	
	export default {
		name: 'Pop-up',
		props:['coinData'],
		emits: ['addclick'],
		data(){
			return{
				selected: this.coinData.filter((item, index) => {
					if(index < 2){
					return item.symbol}}),
			disable: true,
			}
		},
		methods:{
			disabled1(){
				
			}
		}

	}
</script>
<style scoped>
	.coins-container {
		display: flex,block;
		justify-content: center;
		position: absolute;
		margin-top: auto;
		top: 20%;
		left: 10%;
		margin-left: -30px;
		padding: 10px;
		background-color: #ffff;
		border-radius: 12px;
		border: black solid 1px;
		overflow-y: scroll;
		width: 90%; 
		height: 600px;
		z-index: 20;
	}
	.select-coin{
		padding: 10px;
		border: black solid 1px;
		display: flex;
		justify-content: space-between;
		border-radius: 10px;
		margin-top: 10px;
	}
	.button-add{
		background-color: rgb(99, 201, 99);
		border-radius: 5px;
		width: 50px;
	}
	.search{
		display: flex;
		justify-content: space-between;
		border-radius: 10px;
		margin-top: 10px;
	}
</style>