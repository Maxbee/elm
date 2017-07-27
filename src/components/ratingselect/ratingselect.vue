<template>
	<div class="ratingselect">
		<div class="rating-type">
			<span class="block all" :class="{'active':selectType===2}">{{desc.all}}<span class="rtcount">1</span></span>
			<span class="block positive" :class="{'active':selectType===0}">{{desc.positive}}<span class="rtcount">1</span></span>
			<span class="block negative" :class="{'active':selectType===1}">{{desc.negative}}<span class="rtcount">1</span></span>
		</div>
		<div class="switch" :class="{'showon':onlyContent===true}">
			<span class="icon-check_circle"></span>
			<span class="ratingText">只看有内容的评价</span>
		</div>
	</div>
</template>

<script type="text/javascript">
	const POSITIVE = 0;
	const NEGATIVE =1;
	const ALL =2;
	export default{
		props:{
			ratings:{
				type:Array,
				default(){
					return [];
				}
			},
			selectType:{
				type:Number,
				default:ALL
			},
			onlyContent:{
				type:Boolean,
				default:false
			},
			desc:{
				type:Object,
				default(){
					return {
						all:'全部',
						postive:'满意',
						negative:'不满意'
					}
				}
			}
		}
	}
</script>

<style type="text/css">
	.ratingselect{

	}
	.rating-type{
		padding: 18px 0;
		margin: 0 18px;
		font-size: 0;
		border-bottom: 1px solid rgba(7,17,27,0.1);
	}
	.block{
		display: inline-block;
		padding: 8px 12px;
		font-size: 12px;
		margin-right: 8px;
		border-radius: 1px;
		color: rgb(77,85,93);
		line-height: 16px;
	}
	.block .active{
		color: #fff;
	}
	.positive{
		background-color: rgba(0,160,220,0.2);
	}
	.negative{
		background-color: rgba(77,85,93,0.2);
	}
	.rtcount{
		font-size: 8px;
		margin-left: 2px;

	}
	.positive .active{
		background: rgba(0,160,220);
		color: #fff;
	}
	.negative .active{
		background: rgb(77,85,93);
		color: #fff;
	}
	.all {
		background-color: rgb(0,160,220);
		color: #fff;
	}
	.all .active{
		color: rgb(77,85,93);
	}


	.switch{
		padding: 12px 18px;
		line-height: 24px;
		border-bottom: 1px solid rgba(7,17,27,0.1);
		color:rgb(147,153,159);
		font-size: 0;
	}
	.showon .icon-check_circle{
		color:  #00c850;
	}
	.icon-check_circle{
		font-size: 24px;
		margin-right: 4px;

	}
	.ratingText{
		font-size: 12px;
		vertical-align: top;
	}
</style>