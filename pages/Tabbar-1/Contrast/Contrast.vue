<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container p-15 b-b">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<view class="w-100 f-center sticky-box f-between m-b-40">
				<img class="return-img" src="../../../static/tab-2/return-b.png" alt="" @click="back">
				<input @tap="enter2" disabled=true class="input p-l-40 b-b b-c-f8 f-12 c-999" type="text" :placeholder="placeholder">
			</view>
			<view class="w-100 column">
				<image class="back-img w-100 m-b-50" mode="aspectFill" src="../../../static/tab-1/back1.png"></image>
				<view class="view-text m-l-35 f-center j-center m-b-40" @tap="enter1">
					<text class="f-18 c-F54A35">添加对比公司</text>
				</view>
				<text class="f-15 c-999 m-b-15 m-l-35">大家都在对比</text>
				<view class="w-100 p-x-35 b-b f-w">
					<view v-for="(item,i) of lists" :key="i">
						<text class="f-12 c-333 p-10 b-b b-r-2 b-c-f8 m-r-15 m-b-15">{{item}}</text>
					</view>
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
			placeholder:"惠满财数字...",
			lists:["阿里巴巴","网易","腾讯","苹果","三星","百度"],
		}
	},
	methods: {
		back(){
			uni.navigateBack({})
		},
		enter2(){
			uni.navigateTo({
				url:'/pages/Tabbar-1/Contrast/Contrast2'
			})
		},
		enter1(){
			uni.navigateTo({
				url:'/pages/Tabbar-1/Contrast/Contrast1'
			})
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
			.sticky-box {
				position: sticky;
				top: var(--status-bar-height);
				z-index: 99;
			}
			.return-img{
				width:42upx;
				height: 42upx;
			}
			.input{
				width: 626upx;
				height: 60upx;
				border-radius: 30upx;
			}
			.back-img{
				height: 540upx;
			}
			.view-text{
				width: 550upx;
				height: 100upx;
				border: 2upx solid #F54A35;
			}
		}
	}
	
</style>
