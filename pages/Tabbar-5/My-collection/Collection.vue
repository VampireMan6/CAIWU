<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container p-15 b-b">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar m-b-15"></view>
			<view class="w-100 f-center f-between m-b-20">
				<img class="return-img" src="../../../static/tab-2/return-b.png" alt="" @click="back">
				<view class="w-90 f-between">
					<view v-for="(item,i) of lists" :key="i">
						<text @click="Click(i)" :class="i===TabCur?'click':''" class="text b-b f-13 c-999 b-c-f8">{{item}}</text>
					</view>
				</view>
			</view>
			<view class="column w-100 classify">
				<view class="w-100">
					<!-- 资讯 -->
					<Collection1 class="w-100" v-if="TabCur === 0"></Collection1>
					<!-- 指点寻声 -->
					<Collection2 class="w-100" v-else-if="TabCur === 1"></Collection2>
					<!-- 活动 -->
					<Collection3 class="w-100"  v-else-if="TabCur === 2"></Collection3>
					<!-- 公告 -->
					<Collection4 class="w-100"  v-else></Collection4>	
				</view>
				<!-- 触底加载内容 -->
			<!-- 	<view v-show="shows" class="bottom j-center w-100 p-t-10 b-b">
					<text class="c-black3 f-12">没有更多了</text>
				</view>
				<view class="w-100 c-black1 f-15 f-center column p-y-10 b-b">
					<text class="show1" v-if="loading">加载中...</text>
				</view> -->
			</view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 
import Collection1 from './Collection1.vue';
import Collection2 from './Collection2.vue';
import Collection3 from './Collection3.vue'
import Collection4 from './Collection4.vue'

export default {
	data() {
		return {
			lists:["资讯","指点寻声","活动","公告"],
			TabCur:0,
		}
	},
	components: {
		Collection1,
		Collection2,
		Collection3,
		Collection4
	},
	methods: {
		Click(i){
			this.TabCur = i;
		},
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
			.text{
				padding:10upx 30rpx;
				border: 2upx solid #E5E5E5;
			}
			.click{
				background-color: #FFFFFF;
				color: #333333;
			}
		}
	}
	
</style>
