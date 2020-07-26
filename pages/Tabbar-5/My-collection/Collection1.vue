<template>
	<view class="container">
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
</template>
<script>
	
// import util from '../../common/util.js'; 
import Messagelist from '../../../static/json/Messagelist5.json'

export default {
	data() {
		return {
			datas1:Messagelist,
		}
	},
	methods: {
		
	},
};
</script>

<style lang="scss">
	.container{
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
	
</style>
