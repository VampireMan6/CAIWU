<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<view class="w-100 p-15 b-b f-center sticky-box f-between m-b-5">
				<img class="return-img" src="../../../static/tab-2/return-b.png" alt="" @click="back">
				<input @tap="entersearch" disabled="true" class="input p-l-40 b-b b-c-f8 f-12 c-999" type="text" :placeholder="placeholder">
			</view>
			<view class="w-100 column p-x-30 b-b m-b-70">
				<text class="f-15 c-999 m-b-15">我的公司</text>
				<view class="w-100 f-between f-center m-b-20">
					<picker class="picker b-c-f8 b-r-2" :range="arrays1" mode="selector" @change="select1">
						<view class="f-15 view-picker b-b c-333">{{arrays1[arrayIndex1]}}</view>
					</picker>
					<img @change="select1" class="img-select" src="../../../static/tab-1/select.png" alt="">
				</view>
				<text class="f-15 c-999 m-b-15">对比公司</text>
				<view class="w-100 f-between f-center m-b-15" v-for="(item,i) of lists" :key="i">
					<view class="picker picker1 b-b b-c-f8 b-r-2 f-center">
						<img class="img-select1" src="../../../static/tab-1/xuanzhong.png" alt="">
						<view class="img-select2 b-r-50"></view>
						<text class="f-15 c-333 m-l-15">{{item}}</text>
					</view>
					<img class="img-select1" src="../../../static/tab-1/jianshao.png" alt="">
				</view>
				<view class="picker b-b b-c-f8 b-r-2 f-center">
					<text class="f-15 c-333 view-picker b-b">+ 添加对比公司</text>
				</view>
			</view>
			<view class="w-100 p-x-15 b-b">
				<view class="w-100 start-text b-r-2 f-center j-center">
					<text class="f-18 c-white">开始对比</text>
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
			arrays1:['上证A股','深证A股','沪深A股'],
			arrayIndex1:0,
			lists:['上证A股','深证A股','沪深A股'],
		}
	},
	methods: {
		back(){
			uni.navigateBack({})
		},
		select1(e){
			this.arrayIndex1 = e.detail.value;
		},
		entersearch(){
			uni.navigateTo({
				url:'/pages/Tabbar-1/Contrast/Contrast2'
			})
		}
	}
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
			.picker{
				width: 570rpx;
				.view-picker{
					padding: 24upx 30upx;
				}
			}
			.picker1{
				padding: 24upx 30upx;
			}
			.img-select{
				width: 18rpx;
				height: 24upx;
			}
			.img-select1{
				width: 32upx;
				height: 32upx;
			}
			.img-select2{
				width: 30upx;
				height: 30upx;
				border: 2upx solid #999999;
			}
			.start-text{
				height: 100upx;
				background-color: #F54A35;
			}
		}
	}
	
</style>
