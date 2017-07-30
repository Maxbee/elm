<template>
	<div class="seller">
		<div class="seller-concent">
			<div class="sellerView">
				<h1 class="sellerTitle">{{seller.name}}</h1>
				<div class="sellerDesc">
					<star :size="48" :score="seller.score" class="sellerStar"></star>
					<span class="sellerText">{{seller.ratingCount}}</span>
					<span class="sellerText">月售{{seller.sellCount}}单</span>
				</div>
				<ul class="remark">
					<li class="sblock">
						<h2>起送家</h2>
						<div class="spendContent">
							<span class="stress">{{seller.minPrice}}元</span>
						</div>
					</li>
					<li class="sblock">
						<h2>商家配价</h2>
						<div class="spendContent">
							<span class="stress">{{seller.deliveryPrice}}元</span>
						</div>
					</li>
					<li class="sblock">
						<h2>平均配送时间</h2>
						<div class="spendContent">
							<span class="stress">{{seller.deliveryTime}}分钟</span>
						</div>
					</li>
				</ul>
				<div class="collect" @click="like">
					<span class="icon-favorite" :class="{'collectActive':collectActive}"></span>
					<span class="collectText">{{favoriteText}}</span>
				</div>
			</div>
			<split></split>
			<div class="sellerbulletin">
				<h1 class="bulltitle">活动与公告</h1>
				<div class="bullcontentwrap">
					<p class="bullcontent">{{seller.bulletin}}</p>
				</div>
			</div>
		</div>
	</div>
</template>


<script type="text/javascript">
import star from '../star/star';
import split from '../split/split'
	export default{
		props:{
			seller:{
				type:Object
			}
		},
		components:{
			star,split
		},
		data(){
			return {
				collectActive:false
			}
		},
		computed:{
			favoriteText(){
				return this.collectActive?'已收藏':'收藏'
			}
		},
		methods:{
			like(){
				this.collectActive = !this.collectActive 
			}
		}
	}	
</script>
 
<style type="text/css">
	.seller{
		position: absolute;
		top:209px;
		bottom: 46px;
		display: flex;
		width: 100%;
		overflow: hidden;
	}
	.seller-concent{
		width: 100%;
	}
	.sellerView{
		padding: 18px;
		position: relative;
	}
	.sellerTitle{
		font-size: 14px;
		margin-bottom: 8px;
		line-height: 14px;
		color: rgb(7,17,27);
	}
	.sellerDesc{
		line-height: 18px;
		/*font-size: 0;*/

		border-bottom: 1px solid rgba(7,17,27,0.1)
	}
	.sellerStar{
		display: inline-block;
		margin-right: 8px;
		vertical-align: top;
	}
	.sellerText{
		margin-left: 12px;
		display: inline-block;
		vertical-align: top;
		font-size:12px;

	}
	.remark{
		display: flex;
		padding-top: 18px;

	}
	.sblock{
		flex: 1;
		text-align: center;
		border-right: 1px solid rgba(7,17,27,0.1)
	}
	.sblock h2{
		margin-bottom: 4px;
		line-height: 10px;
		font-size: 10px;
		color: rgb(147,153,159);
	}
	.sblock:last-child{
		border:none;
	}
	.spendContent{
		line-height: 24px;
		font-size: 10px;
		color: rgb(7,17,27);
	}
	.stress{
		font-size: 24px;
	}
	.sellerbulletin{
		padding: 18px 18px 0 18px;

	}
	.bulltitle{
		font-size: 14px;
		margin-bottom: 8px;
		line-height: 14px;
		color: rgb(7,17,27);
	}
	.bullcontentwrap{
		padding:0px 12px 16px 12px ;
		border-bottom: 1px solid rgba(7,17,27,0.1)
	}
	.bullcontent{
		line-height: 24px;
		font-size: 12px;
		color: rgb(240,24,14);
	}
	.collect{
		position: absolute;
		right: 18px;
		top: 18px;
		width: 50px;
		text-align: center;
	}
	.icon-favorite{
		display: block;
		color: #d4d6d9;
		font-size:24px;
		line-height: 24px;
		margin-bottom: 4px;
	}
	.collectText{
		line-height: 10px;
		font-size: 10px;
		color: rgb(77,85,93);
	}
	.collectActive{
		color: red;
	}
</style>