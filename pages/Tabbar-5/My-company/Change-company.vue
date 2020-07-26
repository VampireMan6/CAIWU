<template>
	<view class="w-100 containers p-b-20 b-b column">
		<view class="fixed nav"></view>
		<view class="container b-b">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<view class="w-100 f-between f-center b-c-w sticky-box p-15 b-b">
				<img class="return-img" src="../../../static/tab-2/return-b.png" alt="" @click="back">
				<text class="f-17 c-333">新建公司</text>
				<text class="f-13 c-F54A35">更改信息</text>
				<!-- <text class="f-13 c-F54A35">确认</text> -->
			</view>
			<view class="w-100 p-x-20 b-b column">
				<view class="logo b-r-2 m-b-30" @tap="chooseImage1">
					<image mode="aspectFit" class="logo-img w-100 h-100" :src="datas1.data[id].img" ></image>
				</view>
				<!-- 公司名称 -->
				<view class="w-100 column">
					<input type="text" class="w-100 f-15 c-333 m-b-10" v-model="input1" placeholder-style="f-15 c-999" placeholder="请输入公司名称的全称">
					<view class="border-1 m-b-25"></view>
				</view>
				<!-- 省份城市 -->
				<view class="w-100 column">
					<view class="w-100 f-between f-center m-b-10">
						<!-- <input  type="text" class="f-15 c-333 m-b-10" placeholder-style="f-20 c-333" :placeholder="placeholder1"> -->
						<text class="f-15 c-333">{{text1}}</text>
						<img class="enter-img m-l-10" src="../../../static/tab-1/enter.png">
					</view>
					<view class="border-1 m-b-25"></view>
				</view>
				<!-- 行业 -->
				<view class="w-100 column">
					<view class="w-100 f-between f-center m-b-10">
						<!-- <input disabled=fasle type="text" class="f-15 c-333 m-b-10" placeholder-style="f-15 c-333" :placeholder="placeholder2"> -->
						<text class="f-15 c-333">{{text2}}</text>
						<img class="enter-img m-l-10" src="../../../static/tab-1/enter.png">
					</view>
					<view class="border-1 m-b-25"></view>
				</view>
				<!-- 人员规模 -->
				<view class="w-100 column">
					<view class="w-100 f-between f-center m-b-10">
						<!-- <input disabled=fasle type="text" class="f-15 c-333 m-b-10" placeholder-style="f-15 c-333" :placeholder="placeholder3"> -->
						<text class="f-15 c-333">{{text3}}</text>
						<img class="enter-img m-l-10" src="../../../static/tab-1/enter.png">
					</view>
					<view class="border-1 m-b-25"></view>
				</view>
				<!-- 报表会计准则 -->
				<view class="w-100 column">
					<view class="w-100 f-between f-center m-b-10">
						<!-- <input disabled=fasle type="text" class="f-15 c-333 m-b-10" placeholder-style="f-15 c-333" :placeholder="placeholder4"> -->
						<text class="f-15 c-333">{{text4}}</text>
						<img class="enter-img m-l-10" src="../../../static/tab-1/enter.png">
					</view>
					<view class="border-1 m-b-25"></view>
				</view>
				<!-- 公司联系人 -->
				<view class="w-100 column">
					<input type="text" class="f-15 c-333 m-b-10" placeholder-style="f-15 c-999" v-model="input2" placeholder="公司联系人">
					<view class="border-1 m-b-25"></view>
				</view>
				<!-- 联系电话 -->
				<view class="w-100 column">
					<input type="text" class="f-15 c-333 m-b-10" placeholder-style="f-15 c-999" v-model="input3" placeholder="联系电话">
					<view class="border-1 m-b-25"></view>
				</view>
				<!-- 邮箱 -->
				<view class="w-100 column">
					<input type="text" class="f-15 c-333 m-b-10" placeholder-style="f-15 c-999" v-model="input4" placeholder="邮箱">
					<view class="border-1 m-b-25"></view>
				</view>
				<!-- 备注内容 -->
				<view class="w-100">
					<textarea class="p-x-5 b-b f-15 c-333" placeholder-style="f-15 c-999" auto-height v-model="input5" placeholder="备注内容…"/>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 
import companyList from '../../../static/json/Messagelist1.1.json'

export default {
	onLoad(option) {
		this.id = option.id;
	},
	onShow() {
		this.input1 = this.datas1.data[this.id].name;
		this.input2 = this.datas1.data[this.id].people;
		this.input3 = this.datas1.data[this.id].tel;
		this.input4 = this.datas1.data[this.id].email;
		this.input5 = this.datas1.data[this.id].title;
		this.text1 = this.datas1.data[this.id].address;
		this.text3 = this.datas1.data[this.id].number;
	},
	data() {
		return {
			image:"",
			imgss:"",
			imgs:"",
			id:"",
			datas1:companyList,
			input1:"",input2:"",input3:"",input4:"",input5:"",
			text1:"省份城市",text2:"行业",text3:"人员规模",text4:"报表会计准侧",
		}
	},
	methods: {
		back(){
			uni.navigateBack({})
		},
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
			.sticky-box {
				position: sticky;
				top: var(--status-bar-height);
				z-index: 99;
			}
			.return-img{
				width:42upx;
				height: 42upx;	
			}
			.logo{
				width: 200upx;
				height: 140upx;
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
	}
	
</style>
