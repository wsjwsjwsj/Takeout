<template>
  	<div class="goods">
  		<aside ref="menu">
  			<ul>
  				<li v-for="(item, index) in goods" :class="{'current': currentIndex === index}" @click="selectMenu(index)"><span class="text border-1px"><span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>{{item.name}}</span></li>
  			</ul>
  		</aside>
  		<main ref="foods">
  			<ul>
  				<li v-for="item in goods" class="food-list">
  					<h1>{{item.name}}</h1>
  					<ul>
  						<li v-for="food in item.foods" class="food-item border-1px">
  							<img :src="food.icon" alt="" class="food-icon">
  							<div class="content">
  								<h2>{{food.name}}</h2>
  								<p>{{food.description}}</p>
  								<div class="extra">
  									<span>月售{{food.sellCount}}份</span>
  									<span>好评率{{food.rating}}%</span>
  								</div>
  								<div class="price">
  									<span>￥{{food.price}}</span>
  									<span v-show="food.oldPrice">￥{{food.oldPrice}}</span>
  								</div>
  								<cartcontrol :food="food" class="cart"></cartcontrol>   
  							</div>
  						</li>
  					</ul>
  				</li>
  			</ul>
  		</main>
  		<shopcart :delivery-price="seller.deliveryPrice" :min-price="seller.minPrice"></shopcart>
  	</div>
</template>

<script>
import axios from 'axios';
import BScroll from 'better-scroll';
import shopcart from './shopcart';
import cartcontrol from './cartcontrol.vue';

export default {
  	name: 'goods',
  	data (){
    	return {
      		goods: [],
      		listHeight: [],
      		scrollY: 0
    	}
  	},
  	props: {
  		seller: {
  			type: Object
  		}
  	},
  	created() {
  		axios.get('http://127.0.0.1:5000/api/goods', {}).then(res => {
  			if(res.status === 200){
  				this.goods = res.data;
  				this.$nextTick().then(()=>{
                    this.initScroll();
                    this.calcHeight();
                });	  			
  			}
  		}).catch(err => {  			
  			console.log(err);
  		});
  		this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
  	},
  	computed: {
  		currentIndex() {
  			for(let i = 0, len = this.listHeight.length; i < len; i++){
  				let height1 = this.listHeight[i];
  				let height2 = this.listHeight[i+1];
  				if(!height2 || (this.scrollY >= height1 && this.scrollY < height2))
  					return i;
  			}
  			return 0;
  		}
  	},
  	methods: {
  		selectMenu(index){
  			let foodList = this.$refs.foods.querySelectorAll('.food-list');
  			this.foodsScroll.scrollToElement(foodList[index], 300);
  		},
  		initScroll() {
  			this.menuScroll = new BScroll(this.$refs.menu, {
  				click: true
  			});
  			this.foodsScroll = new BScroll(this.$refs.foods, {
  				probeType: 3,
                click: true
  			});
  			this.foodsScroll.on('scroll', (pos)=>{
  				this.scrollY = Math.abs(Math.round(pos.y));
  			});
  		},
  		calcHeight() {
  			let foodList = this.$refs.foods.querySelectorAll('.food-list');
  			let height = 0;
  			this.listHeight.push(height);
  			for(let i = 0, len = foodList.length; i < len; i++){
  				let item = foodList[i];
  				height += item.clientHeight;
  				this.listHeight.push(height);
  			}
  		}
  	},
  	components: {
  		shopcart,
        cartcontrol
  	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.goods{
	width: 100%;
	position: absolute;
	display: flex;
	overflow: hidden;
	top: 174px;
	bottom: 46px;
}
.goods aside{
	width: 80px; 
	background-color: #f3f5f7;
	
}
.goods aside ul li{
	display: table;
	height: 54px;
	width: 80px;
	line-height: 14px;
}
.text{
	display: table-cell;
	width: 56px;
	vertical-align: middle;
	font-size: 12px;
	margin: 0 auto;
	padding: 0 12px;
}
.icon{
	display: inline-block;
	width: 12px;
	height: 12px;
	margin-right: 2px;
	background-size: cover;
	vertical-align: top;
}
.decrease{
	background-image: url('../assets/header/decrease_1@2x.png');
}
.discount{
	background-image: url('../assets/header/discount_1@2x.png');
}
.guarantee{
	background-image: url('../assets/header/guarantee_1@2x.png');
}
.invoice{
	background-image: url('../assets/header/invoice_1@2x.png');
}
.special{
	background-image: url(../assets/header/special_1@2x.png);
}
.goods main{
	flex: 1;
}
.current{
	position: relative;
	margin-top: -1px;
	background-color: #fff;
	font-weight: 700; 
}
.current::after{
	display: none;
}
.food-list h1{
	font-size: 12px;
	color: rgb(147, 153, 159);
	line-height: 26px;
	background-color: #f3f5f7;
	height: 26px;
	padding-left: 14px;
	border-left: 2px solid #d9dde1;  
}
.food-item{
	display: flex;
	margin: 18px;
	padding-bottom: 18px;
}
.food-item:last-child{
	margin-bottom: 0;
}
.food-item:last-child::after{
	display: none;
}
.food-icon{
	width: 57px;
	height: 57px;
	vertical-align: middle;
}
.content{
	margin-left: 10px;
	flex: 1;
    position: relative;
}
.content h2{
	margin-top: 2px;
	font-size: 14px;
	line-height: 14px;
	color: rgb(7, 17, 27);
}
.content p, .extra{
	margin-top: 8px;
	font-size: 10px;
	line-height: 10px;
	color: rgb(147, 153, 159);
}
.extra span:first-child{
	margin-right: 12px;
}
.price{
	line-height: 24px;
	font-weight: 700;
}
.price span:first-child{
	display: inline-block;
	margin-right: 8px;
	font-size: 14px;
	color: rgb(240, 20, 20);
}
.price span:first-child::first-letter, .price span:last-child::first-letter{
	font-size: 10px;
	font-weight: 400;
}
.price span:last-child{
	display: inline-block;
	text-decoration: line-through;
	font-size: 10px;
	color: rgb(7, 17, 27);
}
.cart{
    position: absolute;
    right: 0;
    bottom: 0;
}
</style>