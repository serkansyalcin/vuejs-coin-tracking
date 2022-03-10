<template>
    <div >
        <div v-for="(addedCoin, index) in addedCoins" :key="index" class="addedcoins1">
			<!-- this  remove button emits the remove event to parent components with name removeCoin -->
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
		visibility: visible;
  -webkit-animation: fadeIn 1s;
  animation: fadeIn 1s;
		
	}

.remove{
		background-color: #F8B1AC;
		border: none;
		border-radius: 5px;
		padding: 5px;
		margin-left: 300px;
		cursor: pointer;
		visibility: visible;
  -webkit-animation: fadeOut 1s;
  animation: fadeOut 1s
	}

	@-webkit-keyframes fadeIn {
  from {opacity: 0;} 
  to {opacity: 1;}
}

@keyframes fadeIn {
  from {opacity: 0;}
  to {opacity:1 ;}
}

@-webkit-keyframes fadeOut {
  from {opacity: 1;} 
  to {opacity: 0;}
}

@keyframes fadeOut {
  from {opacity: 1;}
  to {opacity:0 ;}}
</style>