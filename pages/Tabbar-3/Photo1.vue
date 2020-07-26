<template>
	<view class="container">
		<image class="w-100 img" :src="imgss" mode="aspectFit"></image>
		<view class="w-100 f-between p-x-15 b-b m-b-20">
			<view class="f-center picker1 p-x-15 b-b b-c-f8 b-r-2">
				<picker :range="months" mode="selector" @change="select1">
					<view class="f-13 c-333">{{months[arrayIndex1]}}月</view>
				</picker>
				<img class="img-select m-l-5" src="../../static/tab-1/select.png" alt="">
			</view>
			<view class="f-center picker1 p-x-15 b-b b-c-f8 b-r-2">
				<picker :range="years " mode="selector" @change="select2">
					<view class="f-13 c-333">{{years[arrayIndex2]}}年</view>
				</picker>
				<img class="img-select m-l-5" src="../../static/tab-1/select.png" alt="">
			</view>
			<view class="text-view p-x-15 b-b f-center j-center b-c-f8 b-r-2">
				<input class="w-100 f-13 c-333" type="text" placeholder-style="f-13 c-333" placeholder="输入公司名称">
			</view>
		</view>
		<view class="w-100 p-x-15 b-b m-b-20">
			<view class="w-100 f-center j-center botton b-r-2" @tap="enter">
				<text class="f-18 c-white">确认录入</text>
			</view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 

export default {
	onLoad() {
		this.enterphoto()
	},
	data: function(){
		const date = new Date();
		const years  = [];
		const months = []
		for (let i = date.getFullYear(); i >= 1990; i--) {
		    years .push(i)
		}
		for (let i = 1; i <= 12; i++) {
		    months.push(i)
		}
		return {
			imgss:"",
			imgs:"",
			// arrays1:['1月','2月','3月','4月','5月','6月','7月','8月','9月','10月','11月','12月'],
			months,
			arrayIndex1:0,
			// arrays2:[2019,2018,2017,2016,2015,2014],
			years ,
			arrayIndex2:0,
		}
	},
	methods: {
		enterphoto(){
			uni.chooseImage({
			    count: 1, //默认9
			    sizeType: ['original','compressed'], //可以指定是原图还是压缩图，默认二者都有
			    sourceType: ['camera'],
				success:(res)=> {
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
		select1(e){
			this.arrayIndex1 = e.detail.value;
		},
		select2(e){
			this.arrayIndex2 = e.detail.value;
		},
		enter(){
			uni.navigateTo({
				url:'/pages/Tabbar-3/Photo2'
			})
		}
	},
};
</script>

<style lang="scss">
	.container{
		.img{
			height: 1070upx;
		}
		.picker1{
			height: 76rpx;
			.img-select{
				width: 16rpx;
				height: 24upx;
			}
		}
		.text-view{
			width: 310rpx;
			height: 76upx;
		}
		.botton{
			height: 100upx;
			background-color: #F54A35;
		}
	}
	
</style>
