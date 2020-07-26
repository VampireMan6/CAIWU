<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container b-b">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar m-b-15"></view>
			<view class="w-100 top f-between f-center m-b-25">
				<view class="view-left f-center">
					<img @tap="headimg" mode="aspectFill" class="headimg b-r-50" src="../../static/tab-1/head5.jpg" alt="">
					<view class="column m-l-15">
						<text @tap="name" class="f-20 c-333 f-w-600 m-b-10">用户昵称</text>
						<view class="f-13 c-999">
							<text>账户 :</text>
							<text class="m-l-10">{{tel}}</text>
						</view>
					</view>
				</view>
				<view class="view-right m-r-5">
					
				</view>
			</view>
			<view class="w-100 VIPmembers b-r-2 f-between f-center p-x-20 b-b m-b-35">
				<view class="view-left f-center">
					<text class="f-16 c-FFD06D">我的会员</text>
				</view>
				<view class="view-right">
					<text class="f-12 c-FFD06D">年度VIP</text>
					
				</view>
			</view>
			<!-- 底部内容 -->
			<view class="w-100 column">
				<view class="bottom-content column w-100" v-for="(item,i) in list1" :key="i" @tap="enter1(i)">
					<view class="f-between f-center">
						<text class="f-15 c-black">{{item}}</text>
						<view class="right f-center f-center">
							<img class="enter-img m-l-10" src="../../static/tab-1/enter.png">
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="border-3 m-y-20"></view>
		<view class="bottom-contents column p-x-15 b-b m-b-35" v-for="(item,j) in list2" :key="j" @tap="enter2(j)">
			<view class="f-between f-center">
				<text class="f-15 c-black">{{item}}</text>
				<view class="right f-center f-center">
					<img class="enter-img m-l-10" src="../../static/tab-1/enter.png">
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
			list1:["我的公司","我的收藏","报告记录"],
			list2:["账户设置","通知设置","意见反馈"],
			tel:13845784578
		}
	},
	methods: {
		headimg(){//修改头像
			uni.navigateTo({
				url:'/pages/Tabbar-5/Headimg'
			})
		},
		name(){//修改昵称
			uni.navigateTo({
				url:'/pages/Tabbar-5/Name'
			})
		},
		enter1(i){
			if(i == 0){//进入 我的公司
				uni.navigateTo({
					url:'/pages/Tabbar-5/My-company/My-company'
				})
			}else if(i == 1){//进入 我的收藏
				uni.navigateTo({
					url:'/pages/Tabbar-5/My-collection/Collection'
				})
			}else{//进入 报告记录
				uni.navigateTo({
					url:'/pages/Tabbar-5/My-report/Report'
				})
			}
		},
		enter2(j){
			if(j == 0){//进入 账户设置
				uni.navigateTo({
					url:'/pages/Tabbar-5/Set-up/Set-up'
				})
			}else if(j == 1){//进入 通知设置
				uni.navigateTo({
					url:'/pages/Tabbar-5/Set-up/Notice'
				})
			}else{
				uni.navigateTo({//进入 意见反馈
					url:'/pages/Tabbar-5/Set-up/Opinion-feedback'
				})
			}
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
			padding: 30upx 30upx 0 30upx;
			.status_bar {
			    height: var(--status-bar-height);
			    width: 100%;
			}
			.top{
				.view-left{
					width: 540upx;
					height: 120upx;
					.headimg{
						width: 120upx;
						height: 120upx;
					}
				}
				.view-right{
					width: 140upx;
					height: 50upx;
					background-color: #FF9F4C;
				}
			}
			.VIPmembers{
				height: 100upx;
				background-color: rgba(39, 39, 39, 1);
				box-shadow: 0upx -8upx 16upx 0 rgba(0, 0, 0, 0.3);
			}
			// 底部内容
			.bottom-content{
				// position: relative;
				&:not(:last-child) {
					;
					&::after {
						content: '';
						display: block;
						margin-bottom: 70upx;
					}
				}
				.right{
					.fist-img{
						width:30upx;
						height: 26upx;
					}
					.enter-img{
						width:16upx;
						height: 24upx;
					}
				}
			}
		}
		// 底部内容
		.bottom-contents{
			.right{
				.fist-img{
					width:30upx;
					height: 26upx;
				}
				.enter-img{
					width:16upx;
					height: 24upx;
				}
			}
		}
	}
	
</style>
