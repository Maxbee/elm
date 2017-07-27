<template>
	<div class="header">
		<div class="content-wrapper">
			<div class="avatar">
				<img :src="seller.avatar" width="64" height="64">
			</div>

			<div class="content">
				<div class="title">
					<span class="brand"></span>
					<span class="name">{{seller.name}}</span>
				</div>
				<div class="description">
					{{seller.description}}/{{seller.deliveryTime}}分钟送达
				</div>
				<div v-if="seller.supports" class="support">
					<span class="icon" :class="classMap[seller.supports[0].type]"></span>
					<span class="text">{{seller.supports[0].description}}</span>
				</div>
				<div class="support-count" v-if="seller.supports" @click="detailshow=true">
				<span class="count">{{seller.supports.length}}个</span>
				<i class="icon-keyboard_arrow_right"></i>
			</div>	
			</div>
			
		</div>

		<div class="bulletin-wrapper"  @click="detailshow=true">
			<span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
		</div>
		<div class="background">
			<img :src="seller.avatar" width="100%" height="100%">
		</div>

		<div class="detail" v-show="detailshow" transition="fade" >
			<div class="detail-wrapper clearfix">
				<div class="detail-main">
					<h1 class="name">{{seller.name}}</h1>
					<div class="star-wrapper">
						<star :size="48" :score="seller.score"></star>
					</div>
					<div class="title">
						<div class="line"></div>
						<div class="text">优惠信息</div>
						<div class="line"></div>
					</div>
					<ul class="supports" v-if="seller.supports">
						<li class="support-item" v-for="(item ,index) in seller.supports">
							<span class="icon" :class="classMap[seller.supports[index].type]"></span>
							<span class="text">{{item.description}}</span>
						</li>
					</ul>
					<div class="title">
						<div class="line"></div>
						<div class="text">商家公告</div>
						<div class="line"></div>
					</div>
					<div class="bulletin">
						<p class="content">{{seller.bulletin}}</p>
					</div>
				</div>
			</div>
			<div class="detail-close" @click="detailshow=false"><span class="icon-close"></span></div>
		</div>
	</div>
</template>

<script>
import star from '../star/star';

	export default{
		props:{
			seller:{
				type:Object
			}
		},
		data(){
			return{
				detailshow:false
			}
		},
		created:function(){
			this.classMap =['decrease_1','discount_1','guarantee_1','invoice_1','special_1']
		},
		components:{
			star
		}
	}
	
</script>


<style scoped  >
	.clearfix{
	display: inline-block;

	}
.clearfix:after{
	display: block;
	content: '.';
	height:0;
	line-height: 0;
	clear: both;
	overflow: hidden;
}
	body{
		padding: 0;
		margin:0;
	}
	.content-wrapper{
		position: relative;
		padding: 24px  12px 18px 24px;
		font-size: 0;	
		color: #fff;
	
	}
	.avatar{
		display: inline-block;
		
	}
	.avatar img{
		border-radius: 2px;
	}
	.content{
		font-size: 14px;
		display: inline-block;
		margin: 16px;
	}
	.title{
		margin: 2px 0 8px 0;

	}
	.brand{
		display: inline-block;
		width: 30px;
		height: 18px;
		background-image: url(brand@2x.png) ;
		background-size: 100% 100%;
		vertical-align: top;
	}
	.name{
		font-size: 16px;
		margin-left: 6px;
		line-height: 18px;
		font-weight: bold;
	}
	.description{
		margin-bottom: 10px;
		line-height: 12px;
		font-size: 12px;
	}
	.support{

	}
	.icon{
		display: inline-block;
		width: 12px;
		height: 12px;
		margin-right: 4px;
		background-size: 12px 12px;
		background-repeat: no-repeat;
		vertical-align: top;
	}
	.text{
		line-height: 12px;
		font-size: 12px;
		vertical-align: top;
	}
	.decrease_1{
		background-image: url(decrease_1@2x.png);
	}
	.discount_1{
		background-image: url(discount_1@2x.png);
	}
	.guarantee_1{
		background-image: url(guarantee_1@2x.png);
	}
	.invoice_1{
		background-image: url(invoice_1@2x.png);
	}
	.special_1{
		background-image: url(special_3@2x.png);
	}
	.support-count{
		position: absolute;
		right: 12px;
		bottom: 18px;
		padding: 0 8px;
		height: 24px;
		line-height: 24px;
		border-radius: 14px; 
		background:rgba(0,0,0,0.2);
		text-align: center;
	}
	.count{
		font-size: 10px;
	}
	.icon-keyboard_arrow_right{
		font-size: 10px;
		line-height: 24px;
	}

	.bulletin-wrapper{
		background-color: rgba(00,00,00,0.2);
		height: 28px;
		line-height: 28px;
		padding: 0 22px 0 12px;
		white-space: nowrap;
		text-overflow: ellipsis;
		overflow: hidden;
		color: #fff;
	}
	.bulletin-title{
		color: #fff;
		display: inline-block;
		width: 22px;
		height: 12px;
		background-image: url(bulletin@2x.png);
		background-size: 100% 100%;
		background-repeat: no-repeat;
		vertical-align: top;
		margin-top: 8px;
	}
	.bulletin-text{
		font-size: 10px;
		vertical-align: top;
		margin: 0 4px;
	}
	.header{
		position: relative;
		background: rgba(7,17,27,0.5);
		overflow: hidden;
	}
	.background{
		position: absolute;
		top:0;
		left: 0;
		width: 100%;
		height: 100%;
		z-index: -2;
		filter:blur(10px);
	}
	.detail{
		position: fixed;
		top: 0;
		left: 0;
		z-index: 100;
		width: 100%;
		height: 100%;
		overflow: auto;
		background: rgba(7,17,27,0.8);
		transition:  all 0.5s;
		backdrop-filter:blur(10px;);
	}
	.detail .fade-transition{
		opacity: 1;
		background: rgba(7,17,27,0.8);
	}
	.detail .fade-enter,.detail .fade-leave{
		opacity: 0;
		background: rgba(7,17,27,0);
	}
	.detail-wrapper{
		min-height: 100%;
		width: 100%;
		color: #fff;
	}
	.detail-main{
		margin-top: 64px;
		padding-bottom: 64px;
	}
	.detail-close{
		position: relative;
		width: 32px;
		height: 32px;
		margin: -64px auto 0 auto;
		clear: both;
		font-size: 32px;
		cursor: pointer;
		color: #fff;
	}
	.iconClose{
		display: inline-block;
		line-height: 32px;
		width: 32px;
		height: 32px;
		text-align: center;
	}
	.name{
		line-height: 16px;
		text-align: center;
		font: 16px;
		font-weight: 700;
	}
	.star-wrapper{
		margin-top: 18px;
		padding: 2px 0;
		text-align: center;
	}
	.detail-main .title{
		display: flex;
		width: 80%;
		margin: 28px auto 24px auto;
	}
	.detail-main .title .line{
		flex: 1;
		position: relative;
		top: -6px;
		border-bottom: 1px solid rgba(255,255,255,0.5)
	}
	.detail-main .title .text{
		padding: 0 12px;
		font-size: 14px;
		font-weight: 700;
	}
	.supports{
		width: 80%;
		margin: 0 auto

	}
	.supports .support-item{
		list-style: none;
		padding: 0 12px ;
		margin-bottom: 12px;
		font-size: 0;

	}
	.support-item:last_child{
		margin-bottom: 0;
	}
	.supports .support-item .icon{
		display: inline-block;
		width: 16px;
		height: 16px;
		vertical-align: top;
		margin-right: 6px;
		background-size: 16px 16px;
		background-repeat: no-repeat;
	}
	.supports .support-item .text{
		line-height: 16px;
		font-size: 12px;
	}
	.bulletin{
		width: 80%;
		margin: 0 auto	
	}
	.bulletin .content{
		font-size: 12px;
		padding: 0 12px; 
		line-height: 24px;
	}
</style>