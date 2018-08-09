<template>
	<div>
		<i v-show="food.count > 0" class="subtract" @click="subtractCount">-</i>
		<b v-show="food.count > 0" class="count">{{food.count}}</b>
		<i class="add" @click="addCount">+</i>
	</div>
</template>

<script>
import Vue from 'vue';

export default {
  	name: 'cartcontrol',
  	props: {
  		food: {
  			type: Object
  		}
  	},
  	data() {
    	return {
      		
    	}
  	},
  	computed: {

  	},
  	methods: {
  		addCount() {
  			if(!this.food.count)
  				Vue.set(this.food, 'count', 1);
  			else
  				this.food.count++;	
  		},
  		subtractCount() {
  			this.food.count--;
  		}
  	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.add, .subtract{
	display: inline-block;
	font-weight: 700;
	height: 24px;
	width: 24px;
	line-height: 28px;
	font-size: 24px;
	border-radius: 50%;
	text-align: center;
	vertical-align: bottom;
}
.add{
	color: #fff;
	background-color: rgb(0, 160, 220);
}
.count{
	font-size: 10px;
	color: rgb(147, 153, 159);
	font-weight: 400;
	line-height: 24px;
	height: 24px;
	display: inline-block;
	text-align: center;
	padding: 0 6px; 
	
}
.subtract{
	color: rgb(0, 160, 220);
	border: 1px solid rgb(0, 160, 220);
	background-color: #fff;
	box-sizing: border-box;
	line-height: 24px;
}
</style>