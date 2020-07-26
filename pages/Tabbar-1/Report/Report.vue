<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<view class="w-100 p-15 b-b f-center f-between">
				<img class="return-img" src="../../../static/tab-2/return-b.png" alt="" @click="back">
				<image class="share-img" src="../../../static/tab-2/share-b.png" mode=""></image>
			</view>
			<view class="w-100 column text-top b-b">
				<text class="f-25 c-333 m-b-5">出具报告</text>
				<text class="f-12 c-333">我们将根据“十维度”指标数据，</text>
				<text class="f-12 c-333">出具您的一份VIP财务数据分析报告</text>
			</view>
			<image class="back4-img w-100" src="../../../static/tab-1/back4.png" mode=""></image>
			<view class="w-100 p-x-30 b-b column m-b-70">
				<text class="f-13 c-999 m-b-15">选择公司</text>
				<view @tap="select(i)" class="w-100 view f-center p-x-15 b-b b-c-f8 m-b-15 b-r-2" v-for="(item,i) of lists" :key="i">
					<image v-if="tabclick == i" class="xuanzhong-img" src="../../../static/tab-1/xuanzhong.png" mode=""></image>
					<text :class="tabclick == i ? 'click' :''" class="f-15 c-999 m-l-15">{{item}}</text>
				</view>
			</view>
			<view class="w-100 p-x-15 fixed botton b-b m-b-20">
				<view class="view-text w-100 f-center j-center b-r-2">
					<text class="f-18 c-white">出具报告</text>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 

export default {
	data() {
		return {
			lists:['上证A股','深证A股','沪深A股'],
			tabclick:0,
		}
	},
	methods: {
		back(){
			uni.navigateBack({})
		},
		select(e){
			this.tabclick = e;
		}
	},
};
</script>

<style lang="scss">
	.containers{
		.nav{
			width: 100%;
			height: var(--status-bar-height);
			background-color: #FFFFFF;
			z-index: 999;
		}
		.container{
			.status_bar {
			    height: var(--status-bar-height);
			    width: 100%;
			}
			.return-img{
				width:42upx;
				height: 42upx;	
			}
			.share-img{
				width: 44upx;
				height: 44upx;
			}
			.text-top{
				padding: 44upx 130upx;
			}
			.back4-img{
				height: 540upx;
			}
			.view{
				height: 90upx;
				.xuanzhong-img{
					width: 32upx;
					height:32upx;
				}
				.click{
					color: #333333;
				}
			}
			.botton{
				bottom: 20upx;
				.view-text{
					height: 100upx;
					background-color: #D2AD75;
				}
			}
		}
	}
	
</style>
