<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container p-15 b-b">
			<view class="w-100 column sticky-box">
				<!-- 顶部占位符 -->
				<view class="w-100 status_bar m-b-15"></view>
				<view class="w-100 f-center f-between m-b-20">
					<img class="return-img" src="../../static/tab-2/return-b.png" alt="" @click="back">
					<view class="w-90 f-between">
						<view v-for="(item,i) of lists" :key="i">
							<text @click="Click(i)" :class="i===TabCur?'click':''" class="text b-b f-13 c-999 b-c-f8">{{item}}</text>
						</view>
					</view>
				</view>
				<view class="column w-100 classify">
					<view class="w-100">
						<!-- 利润表 -->
						<page1 class="w-100" v-if="TabCur === 0"></page1>
						<!-- 资产负债表 -->
						<page2 class="w-100" v-else-if="TabCur === 1"></page2>
						<!-- 现金流量表 -->
						<page3 class="w-100"  v-else></page3>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 
import page1 from './Page1.vue';
import page2 from './Page2.vue';
import page3 from './Page3.vue';

export default {
	data() {
		return {
			lists:["利润表","资产负债表","现金流量表"],
			TabCur:0,
		}
	},
	components: {
		page1,
		page2,
		page3
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
