<template>
	<div>
		<span v-for="item in classes" :class="[item, starType]"></span>
	</div>
</template>

<script>
const LENGTH = 5;
const CLS_ON = '-on';
const CLS_HALF = '-half';
const CLS_OFF = '-off';
export default {
  	name: 'star',
  	props: {
  		size: {
  			type: Number
  		},
  		score: {
  			type: Number
  		}
  	},
  	computed: {
  		starType() {
  			return 'star-item-' + this.size;
  		},
  		classes() {
  			let result = [];
  			let score = Math.floor(this.score*2)/2;
  			let hasDecimal = score%1 !== 0;
  			let integer = Math.floor(score);
  			for(let i = 0; i < integer; i++)
  				result.push('star-' + this.size + CLS_ON);
  			if(hasDecimal)
  				result.push('star-' + this.size + CLS_HALF);
  			while(result.length < LENGTH)
  				result.push('star-' + this.size + CLS_OFF);
  			return result;
  		}
  	},
  	data() {
    	return {
      		
    	}
  	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.star-item-48, .star-item-36, .star-item-24{
	display: inline-block;
	background-size: cover;
}
.star-item-48{	
	width: 20px;
	height: 20px;
	margin-right: 22px;	
}
.star-48:last-child, .star-36:last-child, .star-24:last-child{
	margin-right: 0;
}
.star-48-on{
	background-image: url(../assets/star/star48_on@2x.png);
}
.star-48-half{
	background-image: url(../assets/star/star48_half@2x.png);
}
.star-48-off{
	background-image: url(../assets/star/star48_off@2x.png);
}
.star-item-36{
 	width: 15px;
	height: 15px;
	margin-right: 6px;
}
.star-36-on{
	background-image: url(../assets/star/star36_on@2x.png);
}
.star-36-half{
	background-image: url(../assets/star/star36_half@2x.png);
}
.star-36-off{
	background-image: url(../assets/star/star36_off@2x.png);
}
.star-item-24{
 	width: 10px;
	height: 10px;
	margin-right: 3px;
}
.star-24-on{
	background-image: url(../assets/star/star24_on@2x.png);
}
.star-24-half{
	background-image: url(../assets/star/star24_half@2x.png);
}
.star-24-off{
	background-image: url(../assets/star/star24_off@2x.png);
}

</style>