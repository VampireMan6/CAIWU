<template>
	<view class="container p-b-20 b-b">
		<view class="top relative">
			<!-- 轮播 -->
			<swiper class="w-100 h-100 m-b-10" :autoplay="true" :interval="3000" :duration="1000" :circular="true" :current="swiperCurrent" @change="changeSwiper">
				<swiper-item v-for="(item,i) in swiperImg" :key="i">
				    <image mode="aspectFill" class="swiper-item w-100 h-100 " :src="item.imgs"></image>
				</swiper-item>
			</swiper>
			<view class="nav-b absolute p-20 b-b">
				<img class="return-img" src="../../static/tab-2/return-b.png" alt="" @click="back">
				<img class="share-img" src="../../static/tab-2/share.png" alt="">
			</view>
			<view class="number-list absolute z-999 f-15 c-white f-w-600">
				<text>{{list[swiperCurrent]}}</text>
				<text>/{{swiperImg.length}}</text>
			</view>
		</view>
		<!-- 公司信息 -->
		<view class="w-100 company-message p-x-15 b-b relative">
			<view class="w-100 view b-r-2 b-c-w column">
				<text v-if="datas1.data[id].name.length<16" class="f-20 c-333 m-l-15 m-t-12">{{datas1.data[id].name}}</text>
				<text v-else class="f-20 c-333 m-l-15 m-t-12">{{datas1.data[id].name.slice(0,13)+'...'}}</text>
				<view class="w-100 f-between">
					<text class="f-13 c-999 m-l-15 m-t-5">数据更新{{datas1.data[id].time}}</text>
					<view class="right h-100 f-center j-center f-10 b-r-2">
						<text>+ 公司对比</text>
					</view>
				</view>
			</view>
		</view>
		<!-- 公司简介 -->
		<view class="w-100 p-x-30 b-b f-15 c-333 column">
			<text class="m-b-10">{{datas1.data[id].title}}</text>
			<text class="f-13 c-999 m-b-5">{{datas1.data[id].tel}}</text>
			<text class="f-13 c-999 m-b-5">{{datas1.data[id].email}}</text>
			<text class="f-13 c-999 m-b-10">{{datas1.data[id].address}}</text>
			<view class="border-1 m-b-10"></view>
			<view class="w-100 f-13 m-b-10">
				<text>上证A股</text>
				<text class="m-l-25">行业名称</text>
				<text class="m-l-25">小会计准则</text>
			</view>
		</view>
		<view class="border-3"></view>
		<!-- 财务数据 -->
		<view class="w-100 column statement" v-for="(item,i) of datas2" :key="i">
			<view class="w-100 p-x-30 b-b column">
				<view class="w-100 top1 p-y-15 b-b f-between f-center">
					<text class="left f-15 c-333">{{item}}</text>
					<view class="f-center right f-center j-center" @tap="enter(i)">
						<text class="f-12">年度数据</text>
						<img class="enter-img m-l-5" src="../../static/tab-1/enter.png">
					</view>
				</view>
				<view class="w-100 bottom f-between m-b-10">
					<view v-for="(item,i) of datas3" :key="i">
						<text class="text f-12 c-333 p-10 b-b b-c-f8 b-r-2">{{item}}</text>
					</view>
				</view>
			</view>
			<view class="border-3"></view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 
import companyList from '../../static/json/Messagelist1.json'

export default {
	onLoad(option) {
		this.id = option.id;
	},
	data() {
		return {
			datas1:companyList,
			datas2:[2019,2018,2017],
			datas3:["第1季度","第2季度","第3季度","第4季度"],
			id:0,
			swiperImg:[//导航栏
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
			list:[1,2,3,4,5,6,7,8],
			current: 0,
			swiperCurrent: 0,
		}
	},
	methods: {
		changeSwiper(e){//轮播图
			this.swiperCurrent = e.detail.current;
		},
		back(){
			uni.navigateBack({})
		},
		enter(i){
			let id = i;
			uni.navigateTo({
				url:('/pages/Tabbar-2/AnnualStatement?id='+id)
			})
		}
	},
};
</script>

<style lang="scss">
	.container{
		.top{
			height: 500upx;
			.nav-b{
				width: 750upx;
				top:var(--status-bar-height);
				.return-img,.share-img{
					width:42upx;
					height: 42upx;	
				}
				.share-img{
					margin-left: 580upx;
				}
			}
			.number-list{
				right: 40upx;
				top: 390upx;
			}
		}
		.company-message{
			top: -30upx;
			z-index: 999;
			.view{
				height: 150upx;
				box-shadow: 0upx 8upx 12upx 0 rgba(0, 0, 0, 0.1);
				.right{
					width: 134upx;
					height: 48upx;
					margin-top: 16upx;
					margin-right: 12upx;
					color: #F54A35;
					background-color: rgba(245, 74, 53, 0.1);
				}
			}
		}
		.statement{
			.top1{
				.right{
					color: #F54A35;
					.enter-img{
						width:12upx;
						height: 20upx;
					}
				}
				
			}
		}
	}
	
</style>
