<template>
	<div class="cartcontrol">
		<transition name="move"><div class="cart-decrease icon-remove_circle_outline box" v-show="food.count>0" @click.stop="decreaseOne" ref="box"></div></transition>
		<div class="cart-count"  v-show="food.count>0">{{food.count}}</div>
		<div class="add icon-add_circle" @click.stop="addOne" ></div>
	</div>	
</template>


<script type="text/javascript">

	export default{
		props:{
			food:{
				type:Object
			}
		},
		
		methods:{
			addOne:function(){
				this.$nextTick(function(){
				// console.log(this.$refs.box.getElementsByClassName('box'))
			})
				// alert(this.$els.aa)
				if(!this.food.count){	
					this.$set(this.food,'count',1)	
				}else{
					this.food.count++;
				}
			},
			decreaseOne:function(){
				if (this.food.count>0) {
					this.food.count--;
				}
			}
		},
		mounted (){
			
		}
	}
</script>

<style type="text/css">
	.cartcontrol{
		font-size: 0;
	}
	.cart-decrease,.add{
		display: inline-block;
		padding: 6px;
		line-height: 24px;
		font-size: 24px;
		color: rgb(0,160,220);

	}
	.cart-count{
		display: inline-block;
		vertical-align: top;
		width: 12px;
		padding-top: 6px;
		line-height: 24px;
		text-align: center;
		font-size: 10px;
		color: rgb(147,153,19);
	}
	.add{
		
	}

	.move-enter-active, .move-leave-active {
	  	opacity: 1;
	  	transform: rotateX(0deg);
	  	transition: all 0.5s;
}
	.move-enter, .move-leave-to  {
		opacity: 0;
		transform: rotateX(360deg);
}

</style>