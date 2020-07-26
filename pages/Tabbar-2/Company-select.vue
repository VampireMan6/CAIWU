<template>
	<view class="container">
		<view class="fixed nav"></view>
		<view class="w-100 column">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar b-b"></view>
			<view class="w-100 top-back f-between p-15 b-b">
				<image class="back-img" src="../../static/tab-1/back-w.png" mode="" @tap="back"></image>
				<view class="view-text j-center">
					<text class="f-17 c-white">38381 家公司符合条件 </text>
				</view>
			</view>
		</view>
		<view class="w-100 column relative content">
			<view class="w-100 p-x-15 b-b m-b-25">
				<!-- 选项 -->
				<view class="nav-top b-b f-13 c-333 w-100 f-between b-c-w b-r-2">
					<view class="f-center">
						<picker :range="arrays1" mode="selector" @change="select1">
							<view class="">{{arrays1[arrayIndex1]}}</view>
						</picker>
						<img @change="select1" class="img-select m-l-5" src="" alt="">
					</view>
					<view class="f-center">
						<picker :range="arrays2" mode="selector" @change="select2">
							<view class="">{{arrays2[arrayIndex2]}}</view>
						</picker>
						<img @change="select2" class="img-select m-l-5" src="" alt="">
					</view>
					<view class="f-center">
						<picker :range="arrays3" mode="selector" @change="select3">
							<view class="">{{arrays3[arrayIndex3]}}</view>
						</picker>
						<img @change="select3" class="img-select m-l-5" src="" alt="">
					</view>
				</view>
			</view>
			<!-- 公司列表 -->
			<view class="companyList w-100 p-x-25 b-b column">
				<view class="w-100 column" v-for="(item,i) of datas1.data" :key="i">
					<view class="w-100 m-b-25 f-between f-center">
						<view @tap="enter(i)" class="view-left">
							<img mode="aspectFill" class="w-100 h-100 b-r-2" :src="item.img" alt="">
						</view>
						<view class="view-right column">
							<view  @tap="enter(i)" class="view-top w-100">
								<text v-if="item.name.length<26" class="f-15 c-333">{{item.name}}</text>
								<text v-else class="f-15 c-333">{{item.name.slice(0,23)+'...'}}</text>
							</view>
							<view class="view-bottom w-100 f-between">
								<view  @tap="enter(i)" class="left h-100 f-10 c-999 f-center">
									<text>{{item.number}}</text>
									<text class="m-l-5">份历史财务数据</text>
								</view>
								<view class="right h-100 f-center j-center f-10 b-r-2">
									<text>+ 公司对比</text>
								</view>
							</view>
						</view>
					</view>
					<view class="border-1 w-100 m-b-25"></view>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 
import companyList from '../../static/json/Messagelist1.json'

export default {
	onShow() {
		uni.setNavigationBarTitle({
		　　title:"12 家公司符合条件"
		})
	},
	data() {
		return {
			arrays1:['上证A股','深证A股','沪深A股'],
			arrays2:['半导体','互联网','物联网','航空航天','区块链','5G','医药行业','网络直播','撒旦法撒旦法'],
			arrays3:['小会计准则','一般企业会计'],
			arrayIndex1:0,
			arrayIndex2:0,
			arrayIndex3:0,
			datas1:companyList,
		}
	},
	methods: {
		select1(e){
			this.arrayIndex1 = e.detail.value;
		},
		select2(e){
			this.arrayIndex2 = e.detail.value;
		},
		select3(e){
			this.arrayIndex3 = e.detail.value;
		},
		enter(i){
			let id = i;
			uni.navigateTo({
				url:('/pages/Tabbar-2/Company-message?id='+id)
			})
		},
		back(){
			uni.navigateBack({})
		}
	},
};
</script>

<style lang="scss">
	.container{
		.nav{
			width: 100%;
			height: var(--status-bar-height);
			background-color: #000000;
			z-index: 999;
		}
		.status_bar {
		     height: var(--status-bar-height);
		     width: 100%;
		}
		.top-back{
			height: 180upx;
			background-color: #000000;
			.back-img{
				width: 24upx;
				height: 44upx;
			}
			.view-text{
				width: 660upx;
			}
		}
		.content{
			top: -84upx;
			z-index: 999;
			.nav-top{
				padding: 32upx 40upx;
				height: 100upx;
				box-shadow: 0upx 8upx 12upx 0 rgba(0, 0, 0, 0.1);
				.img-select{
					width: 18rpx;
					height: 24upx;
					background-color: #007AFF;
				}
			}
			.companyList{
				.view-left{
					width: 200upx;
					height: 140upx;
				}
				.view-right{
					width: 416upx;
					height: 140upx;
					.view-top{
						height: 84upx;
					}
					.view-bottom{
						height: 48upx;
						.right{
							width: 134upx;
							color: #F54A35;
							background-color: rgba(245, 74, 53, 0.1);
						}
					}
				}
			}
		}
	}
	
</style>
