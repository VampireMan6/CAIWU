<template>
	<view class="container">
		<view class="w-100 column top-text b-b">
			<text class="f-27 c-333 f-w-600 m-b-10">十维度 财务分析</text>
			<text class="f-18 c-333">轻松 精准 明确</text>
		</view>
		<image class="w-100 p-x-15 b-b img-back6" src="../../static/tab-1/back6.png" mode=""></image>
		<view class="w-100 imgs b-b f-between f-center">
			<view class="column f-center">
				<image @tap="enterphoto" class="img-camera m-b-10" src="../../static/tab-1/camera.png" mode=""></image>
				<text class="f-15 c-333">拍照录入</text>
			</view>
			<view class="column f-center">
				<image class="img-camera m-b-10" src="../../static/tab-1/file.png" mode=""></image>
				<text class="f-15 c-333">文件上传</text>
			</view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 

export default {
	data() {
		return {
			imgss:"",
			imgs:"",
		}
	},
	methods: {
		enterphoto(){
			uni.navigateTo({
				url:'/pages/Tabbar-3/Photo1'
			})
		}
	},
};
</script>

<style lang="scss">
	.container{
		.top-text{
			padding: 140upx 130upx 0 130upx;
		}
		.img-back6{
			height: 540rpx;
		}
		.imgs{
			padding: 170rpx 140upx;
			.img-camera{
				width: 130upx;
				height: 130rpx;
			}
		}
	}
	
</style>
