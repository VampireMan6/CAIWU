<template>
	<view class="container">
		<image class="back-img w-100" :src="lists.data[id].img"  mode="aspectFill"></image>
		<view class="w-100 column absolute z-999">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<image class="return-img m-l-15 m-t-16" src="../../../static/tab-2/return-b.png" @click="back" mode=""></image>
		</view>
		<view class="w-100 column p-15 b-b">
			<text class="f-20 c-333 m-b-15 f-w-600">{{lists.data[id].name}}</text>
			<text class="f-15 c-333 m-b-20">{{lists.data[id].title}}</text>
			<view class="border-1 m-b-20"></view>
			<view class="w-100 f-center f-between m-b-20">
				<view class="f-13 c-999">
					<text>惠满财</text>
					<text class="m-l-20">{{lists.data[id].number}} 人已读</text>
				</view>
				<image @tap="collection" v-if="show" class="collection-img" src="../../../static/tab-1/collection1-1.png" mode=""></image>
				<image @tap="collection" v-else class="collection-img" src="../../../static/tab-1/collection1-0.png" mode=""></image>
			</view>
			<view class="w-100 p-x-15 b-b f-between f-center share-view b-c-f8 b-r-2 f-12 c-333 m-b-20">
				<text>把财务知识分享给更多的人吧</text>
				<view class="f-center">
					<image class="share-img" src="../../../static/tab-1/share-1.png" mode=""></image>
					<text class="c-999 m-l-5">分享</text>
				</view>
			</view>
			<text>{{lists.data[id].title}}</text>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 
import Messagelist1 from '../../../static/json/Messagelist1.1.json'

export default {
	onLoad(option) {
		this.id = option.id;
	},
	data() {
		return {
			id:"",
			lists:Messagelist1,
			show:true,
		}
	},
	methods: {
		collection(){
			this.show = !this.show
		},
		back(){
			uni.navigateBack({})
		},
	},
};
</script>

<style lang="scss">
	.container{
		.back-img{
			height:500upx
		}
		.status_bar {
		     height: var(--status-bar-height);
		     width: 100%;
		}
		.return-img{
			width:42upx;
			height: 42upx;	
		}
		.collection-img{
			width: 48upx;
			height: 44upx;
		}
		.share-view{
			height: 74upx;
			.share-img{
				width: 24upx;
				height: 24upx;
			}
		}
	}
	
</style>
