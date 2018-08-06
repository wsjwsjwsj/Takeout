<template>
  	<header>
  		<div class="content-wrapper">
  			<img class="avatar" :src="seller.avatar" alt="">
  			<div class="content">
  				<p class="title"><span class="brand"></span>{{seller.name}}</p>
  				<p class="description">{{seller.description}}/{{seller.deliveryTime}}分钟送达</p>
  				<p v-if="seller.supports" class="supports">
  					<span :class="classMap[seller.supports[0].type]" class="icon" ></span>{{seller.supports[0].description}}
  				</p>
  				<div @click="showDetail" v-if="seller.supports" class="count">{{seller.supports.length}}个<i>></i></div>
  			</div>
  		</div>

  		<p class="bulletin-wrapper" @click="showDetail"><span></span>{{seller.bulletin}}<i>></i></p>
  		<img class="background" :src="seller.avatar" alt="">
  		<div v-show="detailShow" class="detail">
  			<h1></h1>
  			<ul>
  				<li></li>
  				<li></li>
  				<li></li>
  				<li></li>
  				<li></li>
  			</ul>
  			<div class=""></div>
  			<div class="bulletin"></div>
  			<i class="close">X</i>
  		</div>
  	</header>
</template>

<script>
export default {
 	name: 'header-nav',
 	props: { 
 		seller: {
 			type: Object
 		}
 	},
  	data() {
    	return {
    		classMap: [],
    		detailShow: false
    	};
  	},
  	created() {
  		this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
  	},
  	methods: {
  		showDetail() {
  			this.detailShow = true;
  		}
  	}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
header{
	width: 100%;
	background-color: rgba(7, 17, 27, 0.5);
	position: relative;
}
.content-wrapper{
	padding: 24px 0 18px 24px;
	overflow: hidden;
}
.avatar{
	display: block;
	width: 64px;
	height: 64px;
	border-radius: 2px;
	padding-right: 16px;
	float: left;
}
.content{
	padding-top: 2px;
	position: relative;
}
.title{
	font-size: 16px;
	color: rgb(255, 255, 255);
	font-weight: 700;
	height: 18px;
	line-height: 18px;
	margin-bottom: 8px;
	
}
.brand{
	color: rgba(7, 17, 27, 0.5);
	margin-right: 6px;
	display: inline-block;
	width: 30px;
	height: 18px;
	background-image: url('../assets/header/brand@2x.png');
	background-size: cover;
	vertical-align: middle;
}
.description{
	font-size: 12px;
	color: #fff;
	font-weight: 200;
	height: 12px;
	line-height: 12px;
	margin-bottom: 10px;
}
.supports{
	font-size: 10px;
	color: #fff;
	font-weight: 200;
	line-height: 12px;
	height: 12px;
}
.icon{
	display: inline-block;
	width: 12px;
	height: 12px;
	margin-right: 4px;
	background-size: cover;
	vertical-align: middle;
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
.count{
	position: absolute;
	box-sizing: border-box;
	bottom: 0px;
	right: 12px;
	padding: 7px 8px;
	height: 24px;
	line-height: 12px;
	font-weight: 200;
	font-size: 10px;
	color: #fff;
	border-radius: 14px; 
	background-color: rgba(0, 0, 0, 0.2);
	text-align: center;
}
.count i{
	display: inline-block;
	height: 10px;
	width: 10px;
	margin-left: 2px;
}
.bulletin-wrapper{
	height: 28px;
	line-height: 28px;
	color: #fff;
	background-color: rgba(7, 17, 27, 0.2);
	padding: 0 22px 0 12px;
	overflow: hidden;
	white-space: nowrap;
	text-overflow: ellipsis;
	font-size: 10px;
	position: relative;
}
.bulletin-wrapper span{
	display: inline-block;
	background-image: url(../assets/header/bulletin@2x.png);
	width: 22px;
	height: 12px;
	background-size: cover;
	margin-right: 4px;
	vertical-align: middle;
}
.bulletin-wrapper i{
	position: absolute;
	font-size: 10px;
	right: 12px;
	top: 1px;
	
}
.background{
	position: absolute;
	width: 100%;
	height: 100%;
	z-index: -1;
	top: 0;
	left: 0;
	filter: blur(10px);
}
.detail{
	position: fixed;
	top: 0;
	left: 0;
	z-index: 100;
	width: 100%;
	height: 100%;
	background-color: rgba(7, 17, 27, 0.8);
}
</style>
