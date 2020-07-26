<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<!-- 顶部 -->
			<view class="w-100 p-15 b-b f-center sticky-box b-c-w">
				<image class="return-img" src="../../../static/tab-2/return-b.png" @click="back" mode=""></image>
				<image class="announcement-img" src="../../../static/tab-1/back5.png" mode=""></image>
			</view>
			
		</view>
	</view>
</template>
<script>

export default {
	data() {
		return {
			
		}
	},
	methods: {
		back(){
			uni.navigateBack({})
		},
		enter(i){
			let id = i;
			uni.navigateTo({
				url:('/pages/Tabbar-1/Announcement/Details?id='+id)
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
				width: 90upx;
				height: 36upx;
				margin-left: 276upx;
			}
			.content{
				border: 2upx solid #E5E5E5;
				.img{
					height: 198upx;
				}
			}
		}
	}
	
</style>
