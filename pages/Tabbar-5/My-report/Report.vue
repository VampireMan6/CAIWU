<template>
	<view class="w-100 column container p-x-15 b-b">
		<view class="w-100 contain m-b-40" v-for="(item,i) of datas1.data" :key="i">
			<view class="left h-100">
				
			</view>
			<view class="right h-100 m-l-15 column">
				<text class="w-100 f-15 c-333 text f-w-600 m-b-5">{{item.name}}</text>
				<text class="f-10 c-333 m-b-25">出具日期: {{item.time}}</text>
				<view class="w-100">
					<text class="f-10 text1 b-r-2 c-F54A35">预览</text>
					<text class="f-10 text1 b-r-2 c-F54A35 m-l-25">下载</text>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 
import Messagelist from '../../../static/json/Messagelist5.json'

export default {
	data() {
		return {
			datas1:Messagelist
		}
	},
	methods: {
		
	},
};
</script>

<style lang="scss">
	.container{
		.contain{
			height: 226upx;
			.left{
				width: 226upx;
				background-color: #007AFF;
			}
			.right{
				width: 416rpx;
				.text{
					height: 84upx;
				}
				.text1{
					padding: 10upx 40rpx;
					background-color: rgba(245, 74, 53, 0.1);
				}
			}
		}
	}
	
</style>
