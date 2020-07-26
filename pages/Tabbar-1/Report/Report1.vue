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
			<!-- 下载报告 -->
			<view class="w-100 p-x-15 fixed botton b-b m-b-20">
				<view class="view-text w-100 f-center j-center b-r-2">
					<text class="f-18 c-white">下载报告</text>
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
			
		}
	},
	methods: {
		back(){
			uni.navigateBack({})
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
