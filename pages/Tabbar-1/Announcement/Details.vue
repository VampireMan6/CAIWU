<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<!-- 顶部 -->
			<view class="w-100 p-15 b-b f-center f-between sticky-box b-c-w">
				<image class="return-img" src="../../../static/tab-2/return-b.png" @click="back" mode=""></image>
				<view>
					<image @tap="collection" v-if="show" class="collection-img" src="../../../static/tab-1/collection1-1.png" mode=""></image>
					<image @tap="collection" v-else class="collection-img" src="../../../static/tab-1/collection1-0.png" mode=""></image>
					<image class="share-img m-l-25" src="../../../static/tab-2/share-b.png" mode=""></image>
				</view>
			</view>
			<view class="w-100 column p-15 b-b column">
				<text class="f-20 c-333 m-b-15">{{lists.data[id].name}}</text>
				<text class="m-b-30">{{lists.data[id].title}}</text>
				<view class="w-100 f-13 c-999 f-between p-x-15 b-b">
					<text>{{lists.data[id].time}}</text>
					<text>阅读 {{lists.data[id].number}}</text>
				</view>
			</view>
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
		back(){
			uni.navigateBack({})
		},
		collection(){
			this.show = !this.show
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
			.collection-img{
				width: 48upx;
				height: 44upx;
			}
			.share-img{
				width: 44upx;
				height: 44upx;
			}
		}
	}
	
</style>
