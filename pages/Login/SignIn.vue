<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container b-b">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<view class="w-100 f-between f-center m-b-60">
				<view>
					<text class="f-30 c-333 f-w-600">注册</text>
					<view class="relative">
						<view class="absolute view1 b-r-50"></view>
						<view class="absolute view2 b-r-50"></view>
					</view>
				</view>
				<view class="f-center" @tap="enter">
					<text class="f-15 c-333">去登录</text>
					<img class="enter-img m-l-10" src="../../static/tab-1/enter.png">
				</view>
			</view>
			<!-- 账号 -->
			<view class="w-100 f-between f-center m-b-10">
				<input type="number" class="w-78 f-20 c-333" v-model="phoneEmail1" maxlength="11" placeholder-style="f-15 c-999" :placeholder="placeholder1">
				<img @tap="delete1" v-if="phoneEmail1.length !==0 " class="delete-img" src="../../static/tab-1/delete1.png" alt="">
			</view>
			<view class="border-2 m-b-50" :class="phoneEmail1.length ==0 ? 'border-2' : 'border-22' "></view>
			<!-- 输入验证码 -->
			<view class="w-100 f-between f-center m-b-10">
				<input type="number" class="w-50 f-20 c-333" v-model="code" maxlength="6" placeholder-style="f-15 c-999" :placeholder="placeholder3">
				<img @tap="delete3" v-if="code.length !==0 " class="delete-img" src="../../static/tab-1/delete1.png" alt="">
				<view v-show="show" class="f-15 ED7059">
					<text class="m-l-5" @click="getCode">发送验证码</text>
				</view>
				<view v-show="!show" class="f-14 c-999">
					<text>{{ count }}s</text>
					<text class="m-l-5">后再发送</text>
				</view>
			</view>
			<view class="border-2 m-b-50" :class="phoneEmail1.length ==0 ? 'border-2' : 'border-22' "></view>
			<!-- 密码 -->
			<view class="w-100 f-between f-center m-b-10">
				<input type="text" :password="password" class="w-78 f-20 c-333" v-model="password1" placeholder-style="f-15 c-999" :placeholder="placeholder2">
				<img @tap="switchstate" v-if="password1.length !==0 " class="show-hidden" :src="'../../static/tab-1/attention'+forbid+'.png'"></img>
				<img @tap="delete2" v-if="password1.length !==0 " class="delete-img" src="../../static/tab-1/delete1.png" alt="">
			</view>
			<view class="border-2 m-b-30" :class="password1.length ==0 ? 'border-2' : 'border-22' "></view>
			<!-- 登录 -->
			<view v-if="phoneEmail1.length !==0 && password1.length !==0 && code.length !==0" class="w-100 button2 f-center j-center m-b-50">
				<text class="f-18">登录1</text>
			</view>
			<view v-else class="w-100 button1 f-center j-center m-b-50">
				<text class="f-18">登录</text>
			</view>
			<view class="w-100 f-between f-center m-b-20">
				<view class="border-4"></view>
				<text class="f-13 c-999">第三方账号登录</text>
				<view class="border-4"></view>
			</view>
			<!-- 微信登录 -->
			<view class="w-100 j-center m-b-40" @tap="weixinlogin">
				<img class="weixin-img m-b-5" src="../../static/tab-1/weixin.png" alt="" />
			</view>
			<view class="w-100 j-center m-b-20">
				<text class="f-13 c-999">登录即同意</text>
				<text class="f-13 c-333 m-l-5">《用户服务协议》</text>
			</view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 

export default {
	data() {
		return {
			placeholder1:"输入账户手机号",
			phoneEmail1:"",
			placeholder2:"输入密码",
			password1:"",
			placeholder3:"输入验证码",
			code:"",
			show:true,
			forbid:"_forbid",
			password:true,
			count:"",
			
		}
	},
	methods: {
		delete1(){
			this.phoneEmail1 = "";
		},
		delete2(){
			this.password1 = "";
		},
		delete3(){
			this.code = "";
		},
		switchstate() {
			if(this.forbid == '_forbid'){
				this.forbid = '';
				this.password = false;
			}else{
				this.forbid = '_forbid';
				this.password = true;
			}
		},
		enter(){//登录页面
			uni.navigateTo({
				url:'/pages/Login/Login'
			})
		},
		getCode(){//发送验证码
			let phone = RegExp(/^1[345678]\d{9}$/).test(this.phoneEmail1);
			if(phone){
				// if(this.phoneEmail1 !== ""){
					// this.getMobile();
					let times = 6;
					if (!this.timer) {
						this.count = times;
						this.show = false;
						this.timer = setInterval(() => {
						if (this.count > 0 && this.count <= times) {
								this.count--;
							} else {
								this.show = true;
								clearInterval(this.timer);
								this.timer = null;
							}
						}, 1000)
					}
				// }
			}else{
				uni.showToast({
					title:'请输入正确的手机号或邮箱',
					duration: 2000,
					icon:"none"
				})
			}
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
			padding: 140rpx 100upx;
			.status_bar {
			     height: var(--status-bar-height);
			     width: 100%;
			}
			.view1{
				width: 24upx;
				height: 24upx;
				background-color: #F54A35;
				z-index: 1;
				top: 10upx;
				left: 10upx;
			}
			.view2{
				width: 12upx;
				height: 12upx;
				background-color: #FFFFFF;
				z-index: 999;
				top: 16upx;
				left: 16upx;
			}
			.enter-img{
				width:12upx;
				height: 20upx;
			}
			.delete-img{
				width: 32rpx;
				height: 32upx;
			}
			.show-hidden{
				width: 32rpx;
				height: 24upx;
			}
			.button1{
				height: 100upx;
				color: #999999;
				background-color: #E5E5E5;
			}
			.button2{
				height: 100upx;
				color: #FFFFFF;
				background-color: #F54A35;
			}
			.border-4{
				width: 164upx;
				height: 2upx;
				background-color: #E5E5E5;
			}
			.weixin-img {
				width: 60upx;
				height: 60upx;
			}
		}
	
	}
</style>
