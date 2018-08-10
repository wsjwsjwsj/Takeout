<template>
  	<footer>
  		<div class="left" @click="toggleList">
  			<div class="logo-wrapper">
  				<i class="logo" :class="{'highlight': totalCount > 0}"></i>
  				<div class="num" v-show="totalCount > 0">{{totalCount}}</div>
  			</div>
  			<p class="price" :class="{'highlight-text': totalPrice > 0}">￥{{totalPrice}}</p>
  			<p class="delv">另需配送费{{deliveryPrice}}元</p>  		
  		</div>
  		<p class="right" :class="payClass">{{payDesc}}</p>
  		<div class="balls">
			<transition-group name="drop">
				<i v-for="(ball, index) in balls" v-show="ball.show" class="ball" :key="index"></i>
			</transition-group>
		</div>
		<transition name="show">
			
			<div class="list" v-show="listShow">
				<div class="list-header">
					<h1>购物车</h1>
					<b @click="clear">清空</b>
				</div>
				<ul>
					<li class="food border-1px" v-for="food in selectedFoods">
						<b class="name">{{food.name}}</b>
						<cartcontrol class="cart" :food="food"></cartcontrol>	
						<b class="food-price">￥{{food.price * food.count}}</b>
					</li>
				</ul>

			</div>

		</transition>
		<transition name="show">
			<div class="background" v-show="listShow"></div>
		</transition>
  	</footer>
</template>

<script>
import cartcontrol from "./cartcontrol.vue";
export default {
  	name: 'shopcart',
  	data() {
    	return {
      		fold: true,
      		balls: [
      			{show: false},
      			{show: false},
      			{show: false},
      			{show: false},
      			{show: false}
      		]
    	}
  	},
  	props: {
  		selectedFoods: {
  			type: Array,
  			default() {
  				return [];
  			}
  		},
  		deliveryPrice: {
  			type: Number,
  			default: 0
  		},
  		minPrice: {
  			type: Number,
  			default: 0
  		}
  	},
  	computed: {
  		totalCount() {
  			let count = 0;
  			this.selectedFoods.forEach((food)=>{
  				count += food.count;
  			});
  			return count;
  		},
  		totalPrice() {
  			let total = 0;
  			this.selectedFoods.forEach((food)=>{
  				total += food.price * food.count;
  			});
  			return total;
  		},
  		payDesc() {
  			if(this.totalPrice === 0){
  				return `￥${this.minPrice}起送`;
  			}else if(this.totalPrice < this.minPrice){
  				let diff = this.minPrice - this.totalPrice;
  				return `还差${diff}元起送`;
  			}else{
  				return '去结算';
  			}
  		},
  		payClass() {
  			if(this.minPrice > this.totalPrice)
  				return 'not-enough';
  			else
  				return 'enough';
  		},
  		listShow() {
  			if(!this.totalCount){
  				this.fold = true;
  				return false;
  			}
  			return !this.fold;
  		}
  	},
  	components: {
  		cartcontrol
  	},
  	methods: {
  		toggleList() {
  			if(!this.totalCount)
  				this.fold = true;
  			this.fold = !this.fold;
  		},
  		clear() {
  			this.selectedFoods.forEach(food=> {
  				food.count = 0;
  			});
  		}
  	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
footer{
	width: 100%;
	height: 48px;
	position: fixed;
	bottom: 0;
	left: 0;
	z-index: 100;
	display: flex;
	background-color: #141d27;
}
.left{
	flex: 1;
}
.logo-wrapper{
	display: inline-block;
	background-color: rgb(43, 52, 60);
	margin: 0 12px;
	padding: 10px;
	width: 56px;
	height: 56px;
	box-sizing: border-box; 
	border-radius: 50%;
	position: relative;
	top: -10px;
}
.logo{
    display: inline-block;
	width: 100%;
	height: 100%;
	border-radius: 50%;
	background-image: url(../assets/goods/shopping_cart.svg);
	background-size: cover;
}
.highlight{
	background-color: rgba(0, 160, 220);
}
.num{
	position: absolute;
	top: 0;
	right: 0;
	width: 24px;
	height: 16px;
	line-height: 16px;
	text-align: center;
	border-radius: 16px;
	font-size: 9px;
	font-weight: 700;
	color: #fff;
	background-color: rgb(240, 20, 20);
	box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4);
}
.price{
	vertical-align: top;
	display: inline-block;
	line-height: 24px;
	height: 24px;
	font-size: 16px;
	font-weight: 700;
	color: rgba(255, 255, 255, 0.4);
	border-right: 1px solid rgba(255, 255, 255, 0.1);
	padding-right: 12px;
	margin-top: 12px;
}
.highlight-text{
	color: #fff;
}
.delv{
	vertical-align: top;
	display: inline-block;
	margin: 14px 0 0 12px;
	font-size: 10px;
	color: rgba(255, 255, 255, 0.4);
}
.right{
	width: 105px;
	height: 48px;
	line-height: 48px;
	font-weight: 700;
	font-size: 12px;
	text-align: center; 
}
.not-enough{
	background-color: #2b333b;
	color: rgba(255, 255, 255, 0.4);
}
.enough{
	background-color: #00b43c;
	color: #fff;
}
.balls{

}
.ball{
	position: fixed;
	left: 32px;
	bottom: 22px;
	z-index: 300;
	width: 16px;
	height: 16px;
	border-radius: 50%;
	background-color: rgb(0, 160, 220);
}
.drop-enter{

}
.drop-enter-active{

}
.drop-enter-to{

}
.list{
	position: absolute;
	top: 0;
	left: 0;
	z-index: -1;
	width: 100%;
	transform: translateY(-100%);

}
.show-enter-active, .show-leave-active{
  	transition: all .5s;
}
.show-enter, .show-leave-to{
  	opacity: 0; 
	transform: translateY(0);
}
.show-enter-to, .show-leave{
	opacity: 1;
}
.list .list-header{
	height: 40px;
	line-height: 40px;
	padding: 0 18px;
	background-color: #f3f5f7;
	border-bottom: 1px solid rgba(7, 17, 27, 0.1);
}
.list-header h1{
	font-size: 14px;
	color: rgb(7, 17, 27);
	float: left;
}
.list-header > b{
	float: right;
	font-size: 12px;
	color: rgb(0, 160, 220);
}
.list ul{
	max-height: 217px;
	background-color: #fff;
	overflow: auto;
	padding: 0 18px;
}
.food{
	height: 48px;
	padding-top: 12px;
	box-sizing: border-box;
}
.name{
	font-size: 14px;
	line-height: 24px;
	color: rgb(7, 17, 27);
	float: left;
}
.food-price{
	font-size: 14px;
	font-weight: 700;
	color: rgb(240, 20, 20);
	line-height: 24px;
	float: right;
	margin: 0 12px 0 18px;
}
.food-price::first-letter{
	font-size: 10px;
	font-weight: 400;
}
.food .cart{
	float: right;
}
.background{
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	z-index: -2;
	background-color: rgba(7, 17, 27, 0.6);
	filter: blur(10px);
}
</style>