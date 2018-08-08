<template>
  	<div id="app">
    	<header-nav :seller="seller">
      
    	</header-nav>
    	<main>
      		<nav class="border-1px">
        		<router-link to='/goods' class="nav-item">商品</router-link>
        		<router-link to='/ratings' class="nav-item">评论</router-link>
        		<router-link to='/seller' class="nav-item">商家</router-link>
      		</nav>

      		<router-view></router-view>
   		</main>  
  	</div>
</template>

<script>
import HeaderNav from '@/components/header-nav';
import axios from 'axios';

export default {
  	name: 'App',
  	data() {
  		return {
  			seller: {}
  		};
  	},
  	created() {
  		axios.get('http://127.0.0.1:5000/api/seller', {}).then(res => {
  			if(res.status === 200){
  				this.seller = res.data;
  			}
  		}).catch(err => {  			
  			console.log(err);
  		});
  	},
  	components: {
  		'header-nav': HeaderNav
  	}
}
</script>

<style>
#app {

}
main nav{
  	width: 100%;
  	height: 40px;
  	line-height: 40px;
  	display: flex;
}
.nav-item{
  	flex: 1; 	
  	text-align: center;
  	font-size: 14px;
  	color: rgb(77, 85, 93);
}
.nav-item:active{
	color: rgb(240, 20, 20);
}

</style>
