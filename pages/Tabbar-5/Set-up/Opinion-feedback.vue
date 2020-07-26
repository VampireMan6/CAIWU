<template>
	<view class="content w-100 column">
		<!-- 反馈类别 -->
		<view class="w-100 top b-b b-c column">
			<text class="f-13 c-999 m-b-10">反馈类别</text>
			<view class="w-100 f-w">
				<view class="view" v-for="(item,i) of datas" :key="i" >
					<text :class="i===tabClicks?'click':''" class="f-13 c-333 b-r-2 text b-c-f8 b-b m-r-20 m-b-20" @tap="tabClick(i)">{{item}}</text>
				</view>
			</view>
		</view>
		<!-- 联系方式 -->
		<view class="w-100 f-between p-20 b-b">
			<text class="f-15 c-333 f-w-600 p-l-5 b-b">联系方式</text>
			<input class="f-15 c-333 t-r" type="text" v-model="tel" placeholder-class="f-15 c-999" placeholder="请输入邮箱或手机号">
		</view>
		<view class="w-100 p-x-20 b-b">
			<view class="border-1"></view>
		</view>
		<!-- 问题和意见 -->
		<view class="w-100 column p-15-20 b-b ">
			<textarea class="p-5 b-b f-12 b-c-f8 c-333 w-100 textarea-height" v-model="content" placeholder-class="C8CDD0" placeholder="请描述您要反馈的意见" />
		</view>
		<!-- 多图上传 -->
		<view class="w-100 f-w p-x-20 b-b">
			<view class="relative" v-for="(item,i) of listimgs" :key="i">
				<img @tap="previewImage(i)" class="img m-r-20 b-r-2" :src="item" alt="">
				<img @tap="delete1(i)" class="img-delete absolute" src="../../../static/tab-1/delect.png" alt="">
			</view>
			<text v-show="show" @tap="shangchuan" class="img-text b-b f-10 c-999 b-c-f8">上传图片</text>
		</view>
		<!-- 提交 -->
		<view class="w-100 p-x-20 b-b m-t-20">
			<view class="exit w-100 f-center p-x-20 b-b j-center t-c" @click="tijiao">
				<text class="f-15 c-white w-100">提交</text>
			</view>
		</view>
	</view>
</template>

<script>
	
// import util from '@/common/util.js'; 

export default {
	data() {
	    return {              
	       datas:["产品BUG","信息举报","账号问题","投诉申请","其他建议"],
		   tabClicks:"",
		   token:"",
		   type:"",
		   content:"",
		   tel:"",
		   listimgs:[],
		   show:true,
	    };
	},
	methods: {
		tabClick(i){
			this.tabClicks=i;
			this.type = this.datas[this.tabClicks];
		},
		tijiao(){
			this.getDatas()
		},
		shangchuan(){
			uni.chooseImage({
			    count: 1, //默认9
			    sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
			    sourceType: ['album','camera'],
				success:(res)=> {
					this.listimgs = this.listimgs.concat(res.tempFilePaths)
					this.imgss = res.tempFilePaths[0];
					if(this.listimgs.length>=9){
						this.show=!this.show;
					}
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
		delete1(i) {//删除图片
			uni.showModal({
				title: "提示",
				content: "是否要删除该图片",
				success: (res) => {
					if (res.confirm) {
						this.listimgs.splice(i, 1)
						// 上传的照片数小于9张，则显示添加照片按钮
						if(this.listimgs.length<9){
							this.show=true
						}
					}
				}
			})
		},
		previewImage(i) {
			//预览图片
			var current = i;
			uni.previewImage({
				current: current,
				urls: this.listimgs
			})
		},
	}
}
</script>


<style lang="scss">
	.content{
		.top{
			padding: 50upx 40upx;
			height: 332upx;
			
			.view{
				.text{
					padding: 20upx 30upx;
				}
				.click{
					color: #FFFFFF;
					background-color: #333333;
				}
			}
		}
		.border{
			height: 20upx;
			background-color: #F8F8F8;
		}
		.textarea-height{
			height:300upx;
		}
		.img{
			width: 120upx;
			height: 120upx;
		}
		.img-delete{
			width: 32upx;
			height: 32upx;
			top:-8upx;
			right: 32upx;
			z-index: 999;
		}
		.img-text{
			padding: 46upx 20upx;
		}
		.exit{
			height: 100upx;
			background-color: #333333;
		}
	}
</style>