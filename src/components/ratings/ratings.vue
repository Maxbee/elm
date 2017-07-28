<template>
	<div class="ratings">
		<div class="ratings-content">
			<div class="overview">
				<div class="viewleft">
					<h1 class="socer">{{seller.score}}</h1>
					<div class="ratingstitle">综合评分</div>
					<div class="rank">高于周边商家{{seller
					.rankRate}}% </div>
				</div>
				<div class="viewright">
					<div class="score-wrap">
						<span class="stitle">服务态度</span>
						<div class="stars"><star :size="48" :score="seller.score"></star></div>
						<span class="serviceScore">{{seller.serviceScore}}</span>			
					</div>
					<div class="score-wrap">
						<span class="stitle">商品评分</span>
					<div class="stars"><star :size="48" :score="seller.foodScore"></star></div>	
						<span class="serviceScore">{{seller.foodScore}}</span>	
					</div>
					<div class="deliverybox">
						<span class="deliverytitle">送达时间</span>
						<span class="deliverytime">{{seller.deliveryTime}}分钟</span>
					</div>
				</div>
			</div>
			
		</div>
		<split></split>
		<ratingselect :select-type="selectType" :only-content="onlyContent"  :ratings="ratings"></ratingselect>
		<div class="commentwrapper">
			<ul>
				<li v-for="rating in ratings" class="useritem">
			<div class="commentavatar">
				<img :src="rating.avatar" width="28" height="28">
			</div>
			<div class="contentss">
				<h1 class="cusername">{{rating.username}}</h1>
				<div class="starw">
					<star :size="48" :score="rating.score"></star>
					<span class="commentdelivery" v-show="rating.rateTime">{{rating.rateTime | formatData}}</span>
				</div>
				<p class="commenttext">{{rating.text}}</p>
				<div class="recommend" v-show="rating.recommend">
					<span class="icon-thumb_up"></span>
					<span v-for="item in rating.recommend" class="tj">
						{{item}}
					</span>
				</div>
				<div class="time"></div>
			</div>
		</li>
			</ul>
		</div>
		
	</div>
</template>

<script type="text/javascript">
import star from '../star/star';
import split from '../split/split';
import ratingselect from '../ratingselect/ratingselect';
import {formatDate} from '../../common/date';


	const ALL =2; 
	const ERR_OK= 0;
	export default{
		props:{
			seller:{
				type:Object
			}
		},
		data(){
			return{
				ratings:[],
				selectType:ALL,
				onlyContent:true
			};
		},
		created(){
			this.$http.get('/api/ratings').then((response)=>{
					response =response.body;
					if(response.errno===ERR_OK){
						this.ratings =response.data
					}
			})
		},
		components:{
			star,split,ratingselect
		},
		filters:{
			formatData(time){
				let date = new Date(time);
				return formatDate(date,'yyyy-MM-dd hh:mm');
			}
		}
	}
</script>

<style type="text/css">
	.ratings{
		position: absolute;
		top: 209px;
		left: 0;
		bottom: 0;
		border:0;
		width:100%;
		overflow: auto;
	}
	.overview{
		display: flex;
		padding: 18px 0;
	}
	.viewleft{
		flex: 0 0 137px;
		width: 137px;
		border-right: 1px solid rgba(7,17,27,0.1);
		text-align: center;
		padding-bottom: 6px 0;
	}
	.socer{
		line-height: 28px;
		font-size: 24px;
		color: rgb(255,153,0);
		margin-bottom: 6px;
	}
	.viewright{
		flex: 1;
		padding-left: 12px;
	}
	.ratingstitle{
		margin-bottom: 8px;
		line-height: 12px;
		font-size: 12px;
		color: rgb(7,17,27);
	}
	.rank{
		line-height: 10px;
		font-size: 10px;
		color: rgb(143,153,159);

	}
	.score-wrap{
		line-height: 18px;
		margin-bottom: 8px;
		font-size: 0;
	}
	.stitle{
		font-size: 12px;
		color: rgb(7,17,27);
		display: inline-block;
		vertical-align: top;
	}

	.deliverytitle{
		font-size: 12px;
		color: rgb(7,17,27，0.1);
		display: inline-block;
		vertical-align: top;
	}
	.stars{
		display: inline-block;
		margin-left: 12px;
		vertical-align: top;
	}
	.serviceScore{
		display: inline-block;
		vertical-align: top;
		line-height: 18px;
		font-size: 12px;
		color: rgb(255,153,0);
	}
	.deliverytime{
		color: rgba(7,17,27,0.5);
		font-size: 12px;
		vertical-align: top;
	}
	.commentwrapper{
		padding: 0 18px;

	}
	.useritem{
		display: flex;
		padding: 18px 0;
		border-bottom: 1px solid rgba(7,17,27,0.1)
	}
	.commentavatar{
		flex:  0 0 28px;
		margin-right: 12px;
	}
	.commentavatar img{
		border-radius: 50%;
	}
	.contentss{
		position: relative;
		flex: 1;
	}
	.cusername{
		line-height: 12px;
		margin-bottom: 4px;
		font-size: 12px;
	}
	.starw{
		margin-bottom: 6px;
		/*font-size: 0;*/
		vertical-align: top;
	}
	.commentdelivery{
		flex: 1
	}
	.commenttext{
		line-height: 18px;
		font-size: 12px;
		margin-bottom: 8px;
	}
	.recommend{
		line-height: 16px;
		line-height: 9px
	}
	.tj{
		display: inline-block;
		margin: 0 8px 4px 0;
		font-size: 9px;
		color: rgb(147,153,159);
		border: 1px solid rgba(7,17,27,0.2);
		border-radius: 1px;
		padding: 3px 6px;
		background-color: #fff;
	}
	.commentdelivery{
		position: absolute;
		top: 0;
		right: 0;
		line-height: 12px;
		font-size: 10px;
		color: rgba(7,17,27,0.2); 
	}
</style>