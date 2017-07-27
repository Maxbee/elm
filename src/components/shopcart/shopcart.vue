<template>
	<div class="shopcart" @click.stop="toggleshow" >
		<div class="shopcontent" >
			<div class="content-left">
				<div class="logo-wrap" >
					<div class="logo" :class="{'lgheightlight':totalCount>0}">
						<span class="shopcartico icon-shopping_cart" ></span>
					</div>
					<div class="cartnum"  v-show="totalCount>0">{{totalCount}}</div>
				</div>

				<div class="shopprice" :class="{'aheightlight':totalPrice>0}">{{totalPrice}}元</div>
				<div class="shopdesc" :class="{'descheightlight':totalPrice>=minPrice}">另需配送费￥{{deliveryPrice}}元</div>
			</div>
			<div class="content-right" @click.stop="toPay">
				<div class="pay" :class="{'canPay':totalPrice>=minPrice}">
					{{payDes}}
				</div>	

			</div>
		</div>
		<div class="ball-container">
			<div v-for="ball in balls" v-show="ball.shaw">
				<div class="innerball"></div>
			</div>
		</div>
		<transition  name="moveup">
			<div class="shopcartlist" :class="{'listshow':listshow}" @click.stop="">
			<div class="list-head">
				<h1 class="listtitle">购物车</h1>
				<span class="clearcart" @click="empty">清空</span>
			</div>
			<div class="list-content">
				<ul>
					<li class="listfood" v-for="food in selectFoods">
						<span class="listname">{{food.name}}</span>
						<div class="listprice">
							<span>￥{{food.price*food.count}}</span>
						</div>
						<div class="cartcontrol-wrap">
							<cartcontrol :food="food"></cartcontrol>
						</div>
					</li>
				</ul>
			</div>
		</div>
		</transition>
	</div>

</template>


<script type="text/javascript">
import cartcontrol from '../cartcontrol/cartcontrol'
	export default{
		data(){
			return{
				balls:[{show:false},{show:false},{show:false},{show:false}],
				fold:true
			}
		},
		props:{
			deliveryPrice:{
				type:Number
			},
			minPrice:{
				type:Number,
				default:0
			},
			selectFoods:{
				type:Array,
				default(){
					return [{
						price:10,
						count:1
					}]
				}		
			}
		},
		methods:{
			toggleshow(){
				if(!this.totalCount){
					return;
				}
				this.fold = !this.fold
			},
			toPay(){
				alert('pay')
			},
			empty(){
				this.selectFoods.forEach((food)=>{
					food.count =0
				})
			}
		},
		computed:{
			totalPrice(){
			  let total =0;
			  this.selectFoods.forEach((food)=>{
			  		total += food.price *food.count;
			  });
			  return total
 			},
 			totalCount(){
 				let count = 0;
 				this.selectFoods.forEach((food)=>{
 					count+= food.count;
 				})
 				return count;
 			},
 			payDes(){
 				if (this.totalPrice===0) {
 					return `￥'${this.minPrice}元起送`
 				}else if(this.totalPrice<this.minPrice){
 					let  diff = this.minPrice -this.totalPrice;
 					return `还差￥${diff}元起送`;
 				}else{
 					return '结算';
 				}
 			},
 			listshow(){
 				if(!this.totalCount){
 					this.fold =true
 					return false
 				}
 				let show =!this.fold;
 				return show;
 			}
		},
		components:{cartcontrol}
	};
</script>


<style type="text/css">
@import '/static/style.css';
	.shopcart{
		position: fixed;
		left: 0;
		bottom: 0;
		z-index: 50;
		width: 100%;
		height: 48px;
		background-color: #000;
	}
	.shopcontent{
		display: flex;
		background-color: #141d27;

	}
	.content-left{
		flex: 1;
	}
	.content-right{
		flex: 0 0 105px;
		width: 105px;
	}
	.logo-wrap{
		position: relative;
		top: -10px;
		margin: 0 12px;
		padding: 6px;
		width: 56px;
		height: 56px;
		display: inline-block;
		border-radius: 50%;
		box-sizing: border-box;
		background-color: #141d27;
	}
	.logo{
		width: 100%;
		height: 100%;
		border-radius: 50%;
		background-color: rgba(0,0,0,0.2);
		text-align: center;
	}
	.shopcartico{
		font-size: 24px;
		color: #80858a;
		line-height: 44px;
	}
	.logo .heightlight{
		background-color: rgb(0,160,220);

	}
	.shopprice{
		display: inline-block;
		vertical-align: top;
		line-height: 24px;
		box-sizing: border-box;
		padding-right: 12px;
		border-right: 1px solid rgba(255,255,255,0.1);
		font-size: 16px;
		font-weight: 700;
		margin-top: 12px;
		color: rgba(255,255,255,0.1);
	}
	.lgheightlight{
		background-color: rgb(0,160,220);
	}
	.shopdesc{
		display: inline-block;
		line-height: 24px;
		margin: 12px 0 0 12px;
		vertical-align: top;
		color: rgba(255,255,255,0.1);
		font-size: 10px;
	}
	.descheightlight{
		color: #fff;
	}
	.pay{
		height: 48px;
		line-height: 48px;
		text-align: center;
		font-size: 12px;
		font-weight: 700;
		color: rgba(255,255,255,0.1);
		background-color: #2b333b;
	}
	.cartnum{
		position: absolute;
		top: 0 ;
		right: 0;
		width: 24px;
		height: 16px;
		line-height: 16px;
		text-align: center;
		border-radius: 16px;
		font-size: 9px;
		font-weight: 700;
		color: #fff;
		background-color: rgb(240,20,20);
		box-shadow: 0 4px 8px 0 rgba(0,0,0,0.4)
	}
	.canPay{
		background-color: #00b43c;
		color:#fff;
	}
	.aheightlight{
		color: #fff;
	}
	.ball-container{

	}
	.immerball{
		position: fixed;
		left: 32px;
		bottom: 22px;
		z-index: 200;
	}

	.shopcartlist{
		position: absolute;;
		top: 0;
		left: 0;
		width: 100%;
		z-index:-1; 
		transition: all 0.5s;
	}
	.list-head{
		height: 40px;
		line-height: 40px;
		padding: 0 18px;
		background-color: #f3f5f7;
		border-bottom: 1px solid rgba(7,17,27,0.1)
	}
	.listtitle{
		float: left;
		font-size: 14px;
		color: rgb(7,17,27);
	}
	.clearcart{
		font-size: 12px;
		color: rgb(0,160,220);
		float: right;
	}
	.list-content{
		padding: 0 18px;
		max-height:217px;
		overflow: auto;
		background-color: #fff;

	}
	.listfood{
		position: relative;
		padding: 12px 0;
		box-sizing: border-box;
		border-bottom: 1px solid rgb(7,17,27,0.1);
	}
	.listname{
		line-height: 24px;
		font-size: 14px;
		color: rgb(7,17,27);
	}
	.listprice{
		position: absolute;
		right: 90px;
		bottom:12px;
		line-height: 24px;
		font-size: 14px;
		font-weight: 700;
		color: rgb(240,20,20);
	}
	.cartcontrol-wrap{
		position: absolute;
		right: 0;
		bottom: 6px;
	}
	.listshow{
		transform: translate3d(0,-100%,0);
	}

/*	.moveup-enter,.moveup-enter-active {
		transform: translate3d(0,-100%,0);
	  	transition: all 0.5s;
}
	 .moveup-leave-active,.moveup-leave-active{
	  
	  	transform: translate3d(0,0,0);
		transition: all 0.5s;
}*/
.moveup-enter-active, .moveup-leave-active{
	 transition: all 1s;
 transform: translate3d(0,-100%,0);

}

/*{
	transition: all 1s;
	transform: translate3d(0,0,0);
		

}*/
/*.moveup-leave-active {
 transform: translate3d(0,0,0);
		transition: all 0.5s;
}
.moveup-enter, .moveup-leave-to{
 transform: translate3d(0,0,0);
		transition: all 0.5s;
}*/
 
</style>