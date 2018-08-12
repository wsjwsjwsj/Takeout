<template>
	<transition name="show">
		<main class="food" v-show="showFlag">
			<img :src="food.image" alt="" class="image">
			<i class="back" @click="show">←</i>
			<div class="name">
				<h2>{{food.name}}</h2>
				<div class="extra">
  					<b>月售{{food.sellCount}}份</b>
  					<b>好评率{{food.rating}}%</b>
  				</div>
				<div class="price">
  					<b>￥{{food.price}}</b>
  					<b v-show="food.oldPrice">￥{{food.oldPrice}}</b>
  				</div>
  				<span class="buy" v-show="!food.count || food.count===0" @click="addFirst">加入购物车</span>
  				<cartcontrol :food="food" class="cart" v-show="food.count && food.count>0"></cartcontrol>
			</div>
			<div class="blank"></div>
			<div class="description">
				<h1>商品介绍</h1>
				<p>{{food.info}}</p>
			</div>
			<div class="blank"></div>
			<div class="ratings">
				<h1>商品评价</h1>
			</div>
		</main>
	</transition>
</template>

<script>
import Vue from 'vue';
import cartcontrol from './cartcontrol.vue';
export default {
  	name: 'food',
  	props: {
  		food: {
  			type: Object
  		}
  		
  	},
  	components: {
  		cartcontrol
  	},
  	data() {
    	return {
    		showFlag: false
    	}
  	},
  	methods: {
  		show() {
  			this.showFlag = !this.showFlag;
  		},
  		addFirst() {
  			Vue.set(this.food, 'count', 1);
  		}
  	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.show-enter, .show-leave-to{
	transform: translateX(100%);
}
.show-enter-active, .show-leave-active{
	transition: transfrom .5s linear;
	transform: translateX(0px);
}
.food{
	position: fixed;
	top: 0;
	left: 0;
	bottom: 48px;
	width: 100%;
	background-color: #fff;
	overflow: auto;
}
.image{
	width: 100%;
}
.back{
	position: absolute;
	top: 10px;
	left: 0;
	font-size: 20px;
	color: #fff;
	display: inline-block;
	padding: 10px;
}
.name{
	margin: 18px;
	position: relative;
}
.name > h2{
	font-size: 14px;
	line-height: 14px;
	color: rgb(7, 17, 27);
	font-weight: 700;
}
.extra{
	font-size: 10px;
	line-height: 10px;
	color: rgb(147, 153, 159);
	margin-top: 8px;
}
.extra b:first-child{
	margin-right: 12px;
}
.price{
	line-height: 24px;
	font-weight: 700;
	margin-top: 16px;
}
.price b:first-child{
	display: inline-block;
	margin-right: 8px;
	font-size: 14px;
	color: rgb(240, 20, 20);
}
.price b:first-child::first-letter, .price b:last-child::first-letter{
	font-size: 10px;
	font-weight: 400;
}
.price b:last-child{
	display: inline-block;
	text-decoration: line-through;
	font-size: 10px;
	color: rgb(7, 17, 27);
}
.buy{
	position: absolute;
	right: 0;
	bottom: 0;
	display: inline-block;
	width: 74px;
	height: 24px;
	line-height: 24px;
	font-size: 10px;
	color: #fff;
	background-color: rgb(0, 160, 220);
	text-align: center;
	border-radius: 12px;
}
.cart{
	position: absolute;
	right: 0;
	bottom: 0;
}
.blank{
	width: 100%;
	height: 16px;
	background-color: #f3f5f7;
	border-top: 1px solid rgba(7, 17, 27, 0.1);
	border-bottom: 1px solid rgba(7, 17, 27, 0.1);
}
.description h1, .ratings h1{
	font-size: 14px;
	font-weight: 400;
	margin: 18px 18px 6px;
}
.description p{
	margin: 0 26px 18px; 
	font-size: 12px;
	color: rgb(77, 85, 93);
	font-weight: 200;
	line-height: 24px;
}
.ratings{

}
</style>