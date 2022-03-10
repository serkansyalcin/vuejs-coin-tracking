<template>
    <div >
        <div v-for="(addedCoin, index) in addedCoins" :key="index" class="addedcoins1">
                    {{addedCoin.symbol}} - {{addedCoin.lastPrice}} - {{addedCoin.weightedAvgPrice}} <span><button class="remove" @click="$emit('removeCoin',addedCoin.symbol)">remove</button></span>
                
        </div>
    </div>
</template>

<script>
export default {
    name: 'AddedCoins',
    props: ['addedCoins'],

}
</script>

<style scoped>
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
		margin-left: 300px;
		cursor: pointer;
	}
</style>