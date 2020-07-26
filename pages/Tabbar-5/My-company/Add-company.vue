<template>
	<view class="container p-25 b-b">
		<view class="logo b-c-f8 b-r-2 relative m-b-30" @tap="chooseImage1">
			<image mode="aspectFill" class="logo-img w-100 h-100" :src="image" ></image>
			<text v-if="image == ''" class="text-logo b-b f-13 c-999 absolute">上传LOGO</text>
		</view>
		<!-- 公司名称 -->
		<view class="w-100 column">
			<input type="text" class="w-100 f-15 c-333 m-b-10" placeholder-style="f-15 c-999" placeholder="*请输入公司名称的全称">
			<view class="border-1 m-b-25"></view>
		</view>
		<!-- 省份城市 -->
		<view class="w-100 column">
			<view class="w-100 f-between f-center m-b-10">
				<input disabled=fasle type="text" class="f-15 c-333 m-b-10" placeholder-style="f-15 c-999" placeholder="*省份城市">
				<img class="enter-img m-l-10" src="../../../static/tab-1/enter.png">
			</view>
			<view class="border-1 m-b-25"></view>
		</view>
		<!-- 行业 -->
		<view class="w-100 column">
			<view class="w-100 f-between f-center m-b-10">
				<input disabled=fasle type="text" class="f-15 c-333 m-b-10" placeholder-style="f-15 c-999" placeholder="*行业">
				<img class="enter-img m-l-10" src="../../../static/tab-1/enter.png">
			</view>
			<view class="border-1 m-b-25"></view>
		</view>
		<!-- 人员规模 -->
		<view class="w-100 column">
			<view class="w-100 f-between f-center m-b-10">
				<input disabled=fasle type="text" class="f-15 c-333 m-b-10" placeholder-style="f-15 c-999" placeholder="人员规模">
				<img class="enter-img m-l-10" src="../../../static/tab-1/enter.png">
			</view>
			<view class="border-1 m-b-25"></view>
		</view>
		<!-- 报表会计准则 -->
		<view class="w-100 column">
			<view class="w-100 f-between f-center m-b-10">
				<input disabled=fasle type="text" class="f-15 c-333 m-b-10" placeholder-style="f-15 c-999" placeholder="*报表会计准则">
				<img class="enter-img m-l-10" src="../../../static/tab-1/enter.png">
			</view>
			<view class="border-1 m-b-25"></view>
		</view>
		<!-- 公司联系人 -->
		<view class="w-100 column">
			<input type="text" class="f-15 c-333 m-b-10" placeholder-style="f-15 c-999" placeholder="公司联系人">
			<view class="border-1 m-b-25"></view>
		</view>
		<!-- 联系电话 -->
		<view class="w-100 column">
			<input type="text" class="f-15 c-333 m-b-10" placeholder-style="f-15 c-999" placeholder="*联系电话">
			<view class="border-1 m-b-25"></view>
		</view>
		<!-- 邮箱 -->
		<view class="w-100 column">
			<input type="text" class="f-15 c-333 m-b-10" placeholder-style="f-15 c-999" placeholder="邮箱">
			<view class="border-1 m-b-25"></view>
		</view>
		<!-- 备注内容 -->
		<view class="w-100 m-b-25">
			<textarea class="p-x-5 b-b f-15 c-333" placeholder-style="f-15 c-999" auto-height placeholder="备注内容…"/>
		</view>
		<!-- 提交 -->
		<view class="w-100 true j-center f-center b-r-2">
			<text class="f-18 c-white">确认新建</text>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 

export default {
	data() {
		return {
			image:"",
			imgss:"",
			imgs:"",
			list:["","*行业","人员规模","*报表会计准则","公司联系人","*联系电话","邮箱"],
		}
	},
	methods: {
		chooseImage1(){//相册选图
			uni.chooseImage({
			    count: 1, //默认9
			    sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
			    sourceType: ['album','camera'],
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
		.logo{
			width: 200upx;
			height: 140upx;
			.text-logo{
				top:50upx;
				left: 30upx;
			}
		}
		.enter-img{
			width:16upx;
			height: 24upx;
		}
		.true{
			height: 100upx;
			background-color: #F54A35;
		}
	}
	
</style>
