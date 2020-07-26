<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container h-100">
			<scroll-view class="h-100" scroll-y="true" :scroll-into-view="toView">
				<!-- 顶部占位符 -->
				<view class="w-100 status_bar"></view>
				<view class="w-100 p-15 b-b f-center sticky-box f-between m-b-5 b-c-w">
					<img class="return-img" src="../../../static/tab-2/return-b.png" alt="" @click="back">
					<input class="input p-l-40 b-b b-c-f8 f-12 c-999" type="text" 
					:placeholder="placeholder"
					v-model="kwords">
				</view>
				<!-- 字母A-Z -->
				<view class="fixed view-fixed">
					<view class="w-100 column f-between f-center">
						<view class="f-12" v-for="(item,c) of datas4" :key="c">
							<view class="f-center j-center b-r-50" :class="c===tabClicks?'click':''" @tap="tabClick(c)">{{item}}</view>
						</view>
					</view>
				</view>
				<!-- 大家都在对比 -->
				<view class="w-100 column p-x-30 b-b m-b-15">
					<text class="f-15 c-999 m-b-15">大家都在对比</text>
					<view class="w-100 f-w">
						<view v-for="(item,i) of lists" :key="i">
							<text class="f-12 c-333 p-10 b-b b-r-2 b-c-f8 m-r-15 m-b-15">{{item}}</text>
						</view>
					</view>
					<view class="border-1"></view>
				</view>
				<!-- 公司列表 -->
				<view class="company-list b-b column">
					<view class="w-100 column" v-for="(item,d) of datas5.data" :key="d">		
						<text :id="'cityletter'+d" class="f-13 c-999 p-y-10 b-b b-c-w">{{item.initial}}</text>
						<view class="w-100 column f-15 c-333 p-y-10 b-b" v-for="(item,e) of item.list" :key="e">
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
import companyList from '../../../static/json/companylist.json'

export default {
	data() {
		return {
			placeholder:"惠满财数字...",
			kwords:"",
			datas4:['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z'],
			tabClicks:0,
			datas5:companyList,
			toView: 'cityletter', //锚链接 初始值
			lists:["阿里巴巴","网易","腾讯","苹果","三星","百度"],
		}
	},
	methods: {
		back(){
			uni.navigateBack({})
		},
		tabClick(c){
			this.tabClicks = c;
			this.toView = "cityletter"+ c;
		},
		enter(a){
			uni.navigateTo({
				url:'/pages/Tabbar-2/Company-select'
			})
		},
	},
	watch:{
	    kwords(){
			console.log(this.kwords)
	    },
	}
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
			.return-img{
				width:42upx;
				height: 42upx;
			}
			.input{
				width: 626upx;
				height: 60upx;
				border-radius: 30upx;
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
