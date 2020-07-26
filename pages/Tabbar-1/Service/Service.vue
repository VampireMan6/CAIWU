<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<!-- 顶部 -->
			<view class="w-100 p-15 b-b f-center sticky-box b-c-w">
				<image class="return-img" src="../../../static/tab-2/return-b.png" @click="back" mode=""></image>
				<image class="announcement-img" src="../../../static/tab-1/back3.png" mode=""></image>
			</view>
			<view class="w-100 p-15 b-b column">
				<view class="w-100 column" v-for="(item,i) of lists.data" :key="i">
					<view class="w-100 p-15 b-b content b-r-2 column m-b-40">
						<image @tap="enter(i)" class="img w-100 b-r-2 m-b-15" v-if="item.img !==''" :src="item.img" mode="aspectFill"></image>
						<text @tap="enter(i)" class="f-15 c-333 m-b-10">{{item.name}}</text>
						<text @tap="enter(i)" class="f-15 c-999">{{item.title}}</text>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 
import Messagelist1 from '../../../static/json/Messagelist1.1.json'

export default {
	data() {
		return {
			lists:Messagelist1
		}
	},
	methods: {
		back(){
			uni.navigateBack({})
		},
		enter(i){
			let id = i;
			uni.navigateTo({
				url:('/pages/Tabbar-1/Service/Details1?id='+id)
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
			.return-img{
				width:42upx;
				height: 42upx;	
			}
			.announcement-img{
				width: 168upx;
				height: 34upx;
				margin-left: 238upx;
			}
			.content{
				box-shadow: 0upx 4upx 16upx 0 rgba(0, 0, 0, 0.1);
				.img{
					height: 198upx;
				}
			}
		}
	}
	
</style>
