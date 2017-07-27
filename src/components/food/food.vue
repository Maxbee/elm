<template>
<transition name="moveleft">
	<div class="food" v-show="showFlag">
		<div class="foodshowcontent">
			<div class="image-header">
				<img :src="food.image">
				<div class="back" @click="hide">
					<i class="icon-arrow_lift"></i>
				</div>
			</div>
			<div class="showcontent">
				<div class="showFoodtitle">{{food.name}}</div>
				<div class="showDetail">
					<span class="showSellcont">月售{{food.sellCount}}份</span>
					<span class="showRating">好评率{{food.rating}}%</span>
				</div>
				<div class="price">
					<span class="new">￥{{food.price}}</span>
					<span class="old" v-show="food.ordPrice"></span>
				</div>
			</div>
			<div class="addcartcontrol-wrap">
				<cartcontrol :food="food"></cartcontrol>
			</div>
			<div class="buy" @click="addfirst" v-show="!food.count || food.count===0">加入购物车</div>
		</div>
		<split v-show="food.info"></split>
		<div class="info" v-show="food.info">
			<h1 class="infoTitle">商品信息</h1>
			<p class="infoText">{{food.info}}</p>
		</div>
		<split></split>
		<div class="showRating">
			<h1 class="ratingTitle">商品评价</h1>
			<ratingselect :select-type="selectType" :only-content="onlyContent" :desc="desc" :ratings="food.ratings"></ratingselect>
			<!-- <div>{{food.ratings}}</div> -->
			<div class="ratingbox">
				<ul v-show="food.ratings && food.ratings.length">
					<li v-for="rating in food.ratings" class="ratingItem">
						<div class="user">
							<span class="username">{{rating.username}}</span>
							<img :src="rating.avatar" class="useravater" width="12" height="12">
						</div>
						<div class="time">{{rating.rateTime}}</div>
						<p class="comment">
							<span :class="{'icon-thumb_up':rating.rateType===0,'icon-thumb_down':rating.rateType===1}"></span>{{rating.text}}
						</p>
					</li>
				</ul>
				<div class="norating" v-show="!food.ratings||food.ratings.length"></div>
			</div>
		</div>
	</div>
	</transition>
</template>

<script type="text/javascript">
import cartcontrol from '../cartcontrol/cartcontrol';
import Vue from 'vue';
import split from '../split/split';
import ratingselect from '../ratingselect/ratingselect';

	const POSITIVE = 0;
	const NEGATIVE =1;
	const ALL =2;
	export default{
		props:{
			food:{
				type:Object
				}
		},
		data(){
			 return{
			 	showFlag:false,
			 	selectType:ALL,
			 	onlyContent:false,
			 	desc:{
			 		all:'全部',
			 		positive:'推荐',
			 		negative:'吐槽'
			 	}
			 }
		},
		methods:{
			show(){
				this.showFlag=true;
				this.selectType =POSITIVE;
				this.onlyContent =true;
				this.$nextTick(function(){
					console.log(this.food)
				})

			},
			hide(){
				this.showFlag=false;
			},
			addfirst(event){
				Vue.set(this.food,'count',1)
			}
		},
		components:{
			cartcontrol,split,ratingselect
		}
	}
</script>

<style type="text/css">
	
	.food{
		position: fixed;
		left: 0;
		top:0;
		width: 100%;
		z-index: 30;
		background: white;
		bottom: 48px;
		overflow: auto;
	}
	.image-header{
		position: relative;
		width: 100%;
		height: 0;
		padding-top: 100%;
	}
	.image-header img{
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
	}
	.back{
		position: absolute;
		top: 10px;
		left: 0;
	}

	.icon-arrow_lift{
		display: block;
		padding: 10px;
		font-size: 20px;
		color: #fff;
	}
	.showcontent{
		padding: 18px;

	}
	.showFoodtitle{
		line-height: 14px;
		margin-bottom: 8px;
		font-size: 14px;
		font-weight: 700;
		color: rgb(7,17,27);
	}
	.showDetail{
		margin-bottom: 18px;
		line-height: 10px;
		font-size: 0;
		height: 10px;
	}
	.showSellcont,.showRating{
		font-size: 10px;
		color: rgb(147,153,159);
	}

	.showSellcont{
		font-size: 10px;
		margin-right: 12px; 
	}
	.foodshowcontent{
		position: relative;
	}
	.addcartcontrol-wrap{
		position: absolute;
		right: 12px;
		bottom: 12px;
	}
	.buy{
		position: absolute;
		right: 18px;
		bottom: 18px;
		z-index: 10;
		height: 24px;
		line-height: 24px;
		padding:0 12px;
		box-sizing: border-box;
		font-size: 10px;
		border-radius: 12px;
		color: #fff;
		background-color: rgb(0,160,220)
	}
	.info{
		padding: 18px;

	}
	.infoText{
		line-height: 24px;
		padding:0 8px;
		font-size: 12px;
		color: rgb(77,85,93);
	}
	.infoTitle{
		line-height: 14px;
		margin-bottom: 6px;
		font-size: 14px;
		color: rgb(7,17,27);
	}
	.showRating{
		padding-top: 18px;

	}
	.ratingTitle{
		line-height: 14px;
		margin-left: 18px;
		font-size: 14px;
		color: rgb(7,17,27);
	}
	.ratingbox{
		padding: 0 18px;
	}
	.ratingItem{
		position: relative;
		padding: 16px 0;
		border-bottom: 1px solid rgba(7,17,27,0.1)
	}
	.user{
		position: absolute;
		right: 0;
		top:16px;
		font-size: 0;
		line-height: 12px;
	}
	.username{
		display: inline-block;
		vertical-align: top;
		font-size: 10px;
		color: rgb(147,153,159);
		margin-right: 6px;
	}
	.useravater{
		border-radius: 50%;

	}
	.time{
		margin-bottom: 6px;
		line-height: 12px;
		font-size: 10px;
		color: rgb(147,153,159);
	}
	.comment{
		line-height: 16px;
		font-size: 12px;
		color: rgb(7,17,27);
	}
	.icon-thumb_up,.icon-thumb_down{
		margin-right: 4px;
		line-height: 16px;
		font-size: 12px;
	}
	.icon-thumb_up{
		color: rgb(0,160,220);
	}
	.icon-thumb_down{
		color: rgb(147,153,155);
	}














	.moveleft-enter-active, .moveleft-leave-active {
	  	transition: all .3s;
	  	transform: translate3d(0,0,0);  
	}	
	.moveleft-enter, .moveleft-leave-to  {
		transition: all .3s;
		transform: translate3d(100%,0,0);
	  	
}
</style>