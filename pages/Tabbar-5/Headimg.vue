<template>
	<view class="container column f-center w-100 b-b">
		<img mode="aspectFill" class="headimg b-r-50 m-b-40" :src="image" alt="">
		<text class="text1 m-b-15 b-c-f8 f-15 c-333 b-r-2" @tap="chooseImage1">相册上传</text>
		<text class="text2 b-c-f8 f-15 c-333 b-r-2" @tap="chooseImage2">拍照</text>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 

export default {
	data() {
		return {
			image:"../../static/tab-1/head5.jpg",
			imgss:"",
			imgs:"",
		}
	},
	methods: {
		chooseImage1(){//相册选图
			uni.chooseImage({
			    count: 1, //默认9
			    sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
			    sourceType: ['album'],
				success:(res)=> {
					this.image =res.tempFilePaths[0];
					this.imgss = res.tempFilePaths[0];
					uni.uploadFile({
					    url : util.apiurl + '/api/common/upload_oss',
						method:"POST",
						header:{'token':this.token},
					    filePath: this.imgss,
					    name: 'file',
					    formData: {
					       'user': 'test'
					    },
					    success:(uploadFileRes)=> {
							this.imgs = JSON.parse(uploadFileRes.data).data.url;
							console.log(this.imgs);
					    }
					})		
				}
			})
		},
		chooseImage2(){//拍照
			uni.chooseImage({
			    count: 1, //默认9
			    sizeType: ['original','compressed'], //可以指定是原图还是压缩图，默认二者都有
			    sourceType: ['camera'],
				success:(res)=> {
					this.image =res.tempFilePaths[0];
					this.imgss = res.tempFilePaths[0];
					uni.uploadFile({
					    url : util.apiurl + '/api/common/upload_oss',
						method:"POST",
						header:{'token':this.token},
					    filePath: this.imgss,
					    name: 'file',
					    formData: {
					       'user': 'test'
					    },
					    success:(uploadFileRes)=> {
							this.imgs = JSON.parse(uploadFileRes.data).data.url;
							console.log(this.imgs);
					    }
					})		
				}
			})
		},
	},
};
</script>

<style lang="scss">
	.container{
		padding: 220upx 126upx;
		.headimg{
			width: 500upx;
			height: 500upx;
		}
		.text1{
			padding: 20upx 60upx;
		}
		.text2{
			padding: 20upx 90upx;
		}
	}
	
</style>
