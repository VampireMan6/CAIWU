<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container h-100">
			<scroll-view class="h-100" scroll-y="true" :scroll-into-view="toView">
				<!-- 顶部占位符 -->
				<view class="w-100 status_bar"></view>
				<!-- 搜索 -->
				<!-- #ifdef APP-PLUS -->
				<view class="w-100 p-x-15 b-b m-y-10 relative">
				<!-- #endif -->
				<!-- #ifdef H5 -->
				<view class="w-100 p-x-15 b-b m-y-10 relative">
				<!-- #endif -->
					<input class="w-100 f-12 b-c-f8 input b-r-15 p-l-40" type="text" placeholder-style="c-999" placeholder="惠满财数字…">
					<img class="img-search absolute" src="../../static/tab-2/search.png" alt="">
				</view>
				<!-- 水平滑动 -->
				<scroll-view class="scroll w-100 p-x-15 b-b" scroll-x="true">
					<view>
						<view class="w-100 m-r-10 b-r-2" v-for="(item,i) of datas1" :key="i">
							<img class="img" :src="item.imgs" alt="">
						</view>
					</view>
				</scroll-view>
				<!-- 上证A股分类 -->
				<view class="w-100 p-15 b-b f-between">
					<view class="view-text1 j-center f-center" v-for="(item,a) of datas2" :key="a" @tap="enter(a)">
						<text class="f-15 c-333">{{item}}</text>
					</view>
				</view>
				<!-- 行业分类 -->
				<view class="w-100 classify1 b-b f-w m-b-10">
					<view class="view-text2 b-r-2 b-b m-r-10 m-b-10" v-for="(item,b) of datas3" :key="b">
						<text class="f-12 c-333">{{item}}</text>
					</view>
				</view>
				<!-- 会计分类 -->
				<view class="w-100 classify2 b-b f-w m-b-10">
					<view class="view-text2 b-r-2 b-b m-r-10 m-b-10" v-for="(item,b) of datas6" :key="b">
						<text class="f-12 c-333">{{item}}</text>
					</view>
				</view>
				<!-- 我的财务数据 -->
				<view class="financial-data b-b f-between f-center column m-l-15 c-white m-b-12">
					<text class="f-27">我的财务数据</text>
					<text class="f-10">和上市公司的财务数据有何区别</text>
				</view>
				<view class="tuoyuan m-l-20 m-b-20"></view>
				<!-- 字母A-Z -->
				<view class="fixed view-fixed">
					<view class="w-100 column f-between f-center">
						<view class="f-12" v-for="(item,c) of datas4" :key="c">
							<view class="f-center j-center b-r-50" :class="c===tabClicks?'click':''" @tap="tabClick(c)">{{item}}</view>
						</view>
					</view>
				</view>
				<!-- 公司列表 -->
				<view class="company-list b-b column">
					<view class="w-100 column" v-for="(item,d) of datas5.data" :key="d">		
						<text class="f-13 c-999 p-y-10 b-b sticky-box b-c-w">{{item.initial}}</text>
						<view :id="'cityletter'+d" class="w-100 column f-15 c-333 p-y-10 b-b" v-for="(item,e) of item.list" :key="e">
							<text>{{item.name}}</text>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 
import companyList from '../../static/json/companylist.json'

export default {
	data() {
		return {
			datas1:[
				{
					"imgs":'../../static/tab-1/build1.jpg'
				},
				{
					"imgs":'../../static/tab-1/build2.jpg'
				},
				{
					"imgs":'../../static/tab-1/build3.jpg'
				},
				{
					"imgs":'../../static/tab-1/build4.jpg'
				}
			],
			datas2:['上证A股公司','深证A股公司','沪深A股公司'],
			datas3:['半导体','互联网','物联网','航空航天','区块链','5G','医药行业','网络直播','撒旦法撒旦法'],
			datas6:['小会计准则','一般企业会计'],
			datas4:['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z'],
			tabClicks:0,
			datas5:companyList,
			toView: 'cityletter', //锚链接 初始值
		}
	},
	methods: {
		tabClick(c){
			this.tabClicks = c;
			this.toView = "cityletter"+ c;
		},
		enter(a){
			uni.navigateTo({
				url:'/pages/Tabbar-2/Company-select'
			})
		}
	},
};
</script>

<style lang="scss">
	.containers{
		height: 100vh;
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
			.input{
				height: 60upx;
			}
			.img-search{
				width: 30upx;
				height: 30upx;
				top: 16upx;
				left: 60upx;
			}
			.scroll{
				.img{
					width: 240upx;
					height: 120rpx;
				}
			}
			.view-text1{
				width: 210upx;
				height: 82upx;
				border: 2upx solid #E5E5E5;
			}
			.classify1,.classify2{
				height: 180upx;
				padding: 0 54upx 0 30upx;
				overflow: hidden;
				.view-text2{
					height: 74upx;
					padding: 20upx 30upx;
					background-color: #F8F8F8;
				}
			}
			.classify2{
				height:74rpx;
			}
			.financial-data{
				padding: 10upx 0;
				letter-spacing: 4upx;
				width: 640upx;
				height: 120upx;
				border-radius: 80upx;
				background-image: linear-gradient(to left, #333333,#000000);
			}
			.tuoyuan{
				width: 622upx;
				height: 12upx;
				border-radius: 50%;
				background-image: linear-gradient(to left, rgba(0, 0, 0, 0),rgba(0, 0, 0, 0.45),rgba(0, 0, 0, 0));
			}
			.view-fixed{
				/* #ifdef APP-PLUS */
				top:400upx;
				/* #endif */
				/* #ifdef H5 */
				top: 356upx;
				/* #endif */
				right: 20upx;
				width: 24upx;
				height: 936upx;
				z-index: 999;
				.click{
					width: 32upx;
					height: 32upx;
					background-color: #F54A35;
					color: #FFFFFF;
				}
			}
			.company-list{
				padding: 0 50upx 0 30upx;
				.sticky-box {
					position: sticky;
					top: var(--status-bar-height);
					z-index: 99;
				}
			}
		}
	}
	
</style>
