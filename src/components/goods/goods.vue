<template>
	<div class="goods">
		<div class="menu-wrapper">
			<ul>
				<li class="menu-item" v-for="item in goods">
					<span class="item-text"><span v-show="item.type>0" class="icon"></span>{{item.name}}</span>
				</li>
			</ul>
		</div>
		<div class="foods-wrapper">
			<ul>
				<li class="food-list" v-for="item in goods">
					<h1 class="food-tittle">{{item.name}}</h1>
					<ul>
						 <li class="food-item" v-for="food in item.foods" @click="selectFood(food,$event)">
						 	<div class="food-icon"><img width="57" height="57" :src="food.icon"></div>
						 	<div class="food-content">
						 		<h1 class="foodname">{{food.name}}</h1>
						 		<p class="fooddesc">{{food.description}}</p>
						 		<div class="extra">
						 			<span>月售:{{food.sellCount}}</span>
						 			<span>好评率:{{food.rating}}%</span>
						 		</div>
						 		<div class="price">
						 			<span class="new">{{food.price}}</span>
						 			<span class="old" v-show="food.ordPrice"></span>
						 		</div>
						 		<div class="cartcontrolwrapper" >
						 			<cartcontrol :food="food"></cartcontrol>
						 		</div>
						 	</div>
						 </li>
					</ul>
				</li>
			</ul>
		</div>
		<shopcart :select-foods="selectFoods" :delivery-price="seller.deliveryPrice" :min-price="seller.minPrice"></shopcart>	
		
		<food  :food="selectedFood" ref="food"></food>
		
	</div>
</template>


<script type="text/javascript">
import shopcart from '../shopcart/shopcart';
import cartcontrol from '../cartcontrol/cartcontrol';
import food from '../food/food';
	export default{
		data(){
			return{
				goods:[],
				selectedFood:{}
			}
		},
		props:{
			seller:{
				type:Object
			}
		},
		methods:{
			selectFood(food,event){
				this.selectedFood = food;
				this.$refs.food.show();
			}
		},
		created:function(){
			this.$nextTick(function () {
		      this.$http.get('/api/goods').then((responed) =>{
		      responed = responed.body
		      if (responed.errno==0) {}   
		      this.goods = responed.data;
		  	console.log(this.goods)
		    })
		  })
		},
		computed:{
			selectFoods(){
				let foods =[];
				this.goods.forEach((good)=>{
					good.foods.forEach((food)=>{
						if(food.count){
							foods.push(food)
						}
					})
				})
				return foods;
			}
		},
		components:{shopcart,cartcontrol,food}
	}
</script>

<style type="text/css">
	h1{
		margin: 0;padding: 0
	}
	.goods{
		position: absolute;
		top:209px;
		bottom: 46px;
		display: flex;
		width: 100%;
		overflow: hidden;
	}
	ul{
		margin: 0;
		padding: 0;
	}
	li{
		list-style: none;
	}
	.menu-item{
		display: table;
		width: 56px;
		height: 54px;
		line-height: 14px;
		list-style: none;	
		padding: 0 12px;

	}
	.item-text{
		display: table-cell;
		width: 56px;
		vertical-align: middle;
		font-size: 12px;
		border-bottom: 1px solid rgba(7,17,27,0.1)
	}
	.menu-wrapper{
		flex:0 0 80px;
		width: 80px;
		background-color: #f3f5f7;
		overflow: auto;
	}	
	.food-tittle{
		padding-left: 14px;
		height: 26px;
		line-height: 26px;
		border-left: 2px solid #d9dde1;
		font-size: 12px;
		color: rgb(147,153,159);
		background-color: #f3f5f7;
	}
	.food-item{
		display: flex;
		position: relative;
		margin: 18px;

		padding-bottom: 1px solid rgba(7,17,27,0.1);
		border-bottom: rgba(7,17,27,0.1);
	}

	.food-item:last-child{
		border:none;
		margin-bottom: 0;	
	}
	.food-content{
		flex:1;
		margin: 0 6px;
	}
	.foodname{
		margin: 2px 0 8px 0;
		height: 14px;
		font-size: 14px;
		line-height: 14px;
		color: rgb(7,17,27);
	}
	.fooddesc, .extra{
		line-height: 10px;
		font-size: 10px;
		color: rgb(147,153,159);
	}
	.fooddesc{
		margin-bottom: 8px;
		line-height: 12px;
	}
	.price{
		font-weight: 700;
		line-height: 24px;
	}
	.new{
		margin-right: 8px;
		font-size: 14px;
		color: rgb(240,20,20);
	}
	.old{
		text-decoration: line-through;
		font-size: 10px;
		color: rgb(147,153,159);
	}

	.foods-wrapper{
		flex: 1;
		overflow: auto;
	}
	.cartcontrolwrapper{
		position: absolute;
		right: 0;
		bottom: 12px;
	}




</style>