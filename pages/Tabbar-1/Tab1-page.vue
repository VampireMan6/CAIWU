<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container p-15 b-b">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<view class="w-100 f-center top m-b-5">
				<view class="w-50">
					<text class="f-w-600 f-20 c-000 text1">惠满财</text>
				</view>
				<view class="w-50 f-between">
					<input disabled=true class="input f-12 p-x-15 b-b c-black b-c-f8 b-r-15" type="text"
					 placeholder-class="c-999" placeholder="惠满财数字…" @click="search">
					 <view class="img-head">
						 <img class="w-100 h-100 b-r-50" src="../../static/tab-1/head5.jpg" alt="">
					 </view>
				</view>
			</view>
			<view class="w-100 f-10 c-333 m-b-15">
				<text>精准分析 |</text>
				<text class="m-l-10">轻松 精准 明确</text>
			</view>
			<view class="w-100 column m-b-30">
				<view class="w-100 m-b-5">
					<view class="block-1 p-15 b-b column c-white">
						<text class="f-15 m-b-8 f-w-600">上市·十维度</text>
						<text class="f-12">根据指标</text>
						<text class="f-12">对上市公司报表解读</text>
					</view>
					<view class="block-2 m-l-5 p-15 b-b column c-white" @tap="enter2">
						<text class="f-15 m-b-8 f-w-600">公司对比</text>
						<text class="f-12">与各大公司</text>
						<text class="f-12">财务数据对比</text>
					</view>
				</view>
				<view class="w-100">
					<view class="block-3 p-15 b-b column c-white">
						<text class="f-15 m-b-8 f-w-600">十维度</text>
						<text class="f-12">数据·图表</text>
						<text class="f-12">惠满财十维度释义备份</text>
					</view>
					<view class="block-4 m-l-5 p-15 b-b column c-white" @tap="enter4">
						<text class="f-15 m-b-8 f-w-600">报告</text>
						<text class="f-12">指标分析</text>
						<text class="f-12">VIP独有财务报告</text>
					</view>
				</view>
			</view>
			<!-- 轮播 -->
			<swiper class="swiper w-100 m-b-10" :autoplay="true" :interval="3000" :duration="1000" :circular="true" :current="swiperCurrent" @change="changeSwiper">
				<swiper-item v-for="(item,i) in swiperImg" :key="i">
				    <image mode="aspectFill" class="swiper-item w-100 h-100 " :src="item.imgs"></image>
				</swiper-item>
			</swiper>
			<!-- 轮播指示点样式修改 -->
			<view class="dots j-center m-b-15">
				<view v-for="(item,index) in swiperImg.length" :key="item">
					<view class="dot m-r-10 b-r-50" :class="index==swiperCurrent ? ' active' : ''"></view>
			    </view>
			</view>
			<!-- 公告 -->
			<view class="w-100 f-between gonggao f-center m-b-30" @tap="Announcement">
				<image class="view1" src="../../static/tab-1/back2.png" mode="aspectFill"></image>
				<view class="view2">
					<text v-if="text1.length<17" class="f-13 c-333">{{text1}}</text>
					<text v-else class="f-13 c-333">{{text1.slice(0,16) + '...'}}</text>
				</view>
				<img class="enter-img m-l-10" src="../../static/tab-1/enter.png">
			</view>
			<!-- 文章 -->
			<view class="w-100 content column">
				<view class="w-100 column" v-for="(item,i) of datas1.data" :key="i">
					<view class="w-100 f-between f-center m-b-20">
						<view class="view-left column">
							<text @tap="enter(i)" v-if="item.title.length<22" class="f-17 content-text1 f-w-600 c-333 w-100 m-b-10">{{item.title}}</text>
							<text @tap="enter(i)" v-else class="f-17 content-text1 f-w-600 c-333 w-100 m-b-10">{{item.title.slice(0,21) + '...'}}</text>
							<view class="w-100 c-999 f-14">
								<text @tap="enter(i)">{{item.time}}</text>
								<text @tap="enter(i)" class="m-l-15">{{item.number}}</text>
								<text @tap="enter(i)" class="m-l-5">阅读</text>
							</view>
						</view>
						<view class="view-right">
							<img @tap="enter(i)" class="w-100 h-100 b-r-2" :src="item.img" alt="">
						</view>
					</view>
					<view class="border-1 m-b-20"></view>
				</view>
			</view>
			<!-- 指点寻声 -->
			<view class="w-100 zhidian b-r-2 p-15 b-b column m-b-20">
				<view @tap="enterservice" class="w-100 f-between f-center m-b-15">
					<image class="img-back3" src="../../static/tab-1/back3.png" mode="aspectFill"></image>
					<img class="enter-img m-l-10" src="../../static/tab-1/enter.png">
				</view>
				<view class="border-2 m-b-15"></view>
				<view class="text m-b-10">
					<text @tap="enterservice" v-if="text1.length<36" class="f-17 f-w-600 c-333">{{text1}}</text>
					<text @tap="enterservice" v-else class="f-17 f-w-600 c-333">{{text1.slice(0,35) + '...'}}</text>
				</view>
				<view class="text">
					<text @tap="enterservice" v-if="text1.length<36" class="f-17 f-w-600 c-999">{{text1}}</text>
					<text @tap="enterservice" v-else class="f-17 f-w-600 c-999">{{text1.slice(0,35) + '...'}}</text>
				</view>
			</view>
			<!-- 活动 -->
			<view class="activity column">
				<view v-for="(item,i) of datas2" :key="i">
					<img mode="aspectFill" class="w-100 m-b-10 height b-r-2" :src="item.imgs" alt="">
				</view>
				<view class="w-100 j-center f-12 c-FF9744 f-center m-b-10" @tap="activity">
					<text>全部活动</text>
					<img class="enter-img m-l-10" src="../../static/tab-1/enter.png">
				</view>
				<view class="border-2 m-b-20 m-l-15"></view>
			</view>
			<!-- 文章 -->
			<view class="w-100 content column">
				<view class="w-100 column" v-for="(item,i) of datas1.data" :key="i">
					<view class="w-100 f-between f-center m-b-20">
						<view class="view-left column">
							<text v-if="item.title.length<22" class="f-17 content-text1 f-w-600 c-333 w-100 m-b-10">{{item.title}}</text>
							<text v-else class="f-17 content-text1 f-w-600 c-333 w-100 m-b-10">{{item.title.slice(0,21) + '...'}}</text>
							<view class="w-100 c-999 f-14">
								<text>{{item.time}}</text>
								<text class="m-l-15">{{item.number}}</text>
								<text class="m-l-5">阅读</text>
							</view>
						</view>
						<view class="view-right">
							<img class="w-100 h-100 b-r-2" :src="item.img" alt="">
						</view>
					</view>
					<view class="border-1 m-b-20"></view>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 
import Messagelist from '../../static/json/Messagelist.json'

export default {
	data() {
		return {
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
			current: 0,
			swiperCurrent: 0,
			text1:"公告标题文本最多十七个字卡萨积分喀斯柯达房间爱可视对讲福克斯就开发撒的咖啡机奥斯卡",
			datas1:Messagelist,
			datas2:[//导航栏
				{
					"imgs":'../../static/tab-1/build1.jpg'
				},
				{
					"imgs":'../../static/tab-1/build2.jpg'
				}
			],
		}
	},
	methods: {
		changeSwiper(e){//轮播图
			this.swiperCurrent = e.detail.current;
		},
		search(){
			uni.navigateTo({
				url:'/pages/Tabbar-1/Search'
			})
		},
		enter2(){//公司对比
			uni.navigateTo({
				url:'/pages/Tabbar-1/Contrast/Contrast'
			})
		},
		enter4(){//报告
			uni.navigateTo({
				url:'/pages/Tabbar-1/Report/Report'
			})
		},
		Announcement(){//公告
			uni.navigateTo({
				url:'/pages/Tabbar-1/Announcement/Announcement'
			})
		},
		enter(i){//公告详情
			let id = i;
			uni.navigateTo({
				url:('/pages/Tabbar-1/Announcement/Details?id='+id)
			})
		},
		enterservice(){//财务服务
			uni.navigateTo({
				url:'/pages/Tabbar-1/Service/Service'
			})
		},
		activity(){//活动
			uni.navigateTo({
				url:'/pages/Tabbar-1/Activity/Activity'
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
			.top{
				.text1{
					letter-spacing: 2.5upx;
				}
				.input{
					width: 260upx;
					height: 60upx;
				}
				.img-head{
					width: 60upx;
					height: 60upx;
				}
			}
			.block-1,.block-3{
				width: 390upx;
				height: 180upx;
				background-color: #6B7298;
				border-radius: 4upx;
				box-shadow: 0upx 8upx 16upx 0 rgba(107, 114, 152, 0.5);
			}
			.block-2,.block-4{
				width: 290upx;
				height: 180upx;
				background-color: #F54A35;
				border-radius: 4upx;
				box-shadow: 0upx 8upx 16upx 0 rgba(245, 74, 53, 0.5);
			}
			.block-3{
				background-color: #3B67E5;
				box-shadow: 0upx 8upx 16upx 0 rgba(59, 103, 229, 0.5);
			}
			.block-4{
				background-color: #D2AD75;
				box-shadow: 0upx 8upx 16upx 0 rgba(210, 173, 117, 0.5);
			}
			/* 轮播样式 */
			.swiper{
			    height: 140upx;
				.swiper-item{
					border-radius: 70upx;
				}
			}
			/* 轮播指示点样式 */
			.dots {
				top:680upx;
			    right:40upx;
			    // z-index: 99;
				
				.dot {//未选中样式
				    width: 10upx;
				    height: 10upx;
					background-color: #999999;
				    transition: all .6s;
				}
				.active {//被选中样式
				    width: 40upx;
				    height: 10upx;
					background-color: #999999;
					border-radius: 8upx;
				}
			}
			// 公告样式
			.gonggao{
				.view1{
					width: 140upx;
					height: 50upx;
				}
				.view2{
					width: 442upx;
					height: 36upx;
				}
				.enter-img{
					width:12upx;
					height: 20upx;
				}
			}
			// 文章内容
			.content{
				.view-left{
					width: 416upx;
					height: 136upx;
					.content-text1{
						height: 80upx;
					}
				}
				.view-right{
					width: 234upx;
					height: 136upx;
				}
			}
			// 指点寻声样式
			.zhidian{
				// height: 320upx;
				border: 2upx solid #E5E5E5;
				box-shadow: 0upx 8upx 20upx 0 rgba(229, 229, 229, 0.8);
				.enter-img{
					width:12upx;
					height: 20upx;
				}
				.text{
					height: 80upx;
				}
				.img-back3{
					width: 112upx;
					height: 24upx;
				}
			}
			// 活动
			.activity{
				.height{
					height: 200upx;
				}
				.enter-img{
					width:12upx;
					height: 20upx;
				}
				.border-2{
					width: 630upx;
				}
			}
		}
	}
	
</style>
