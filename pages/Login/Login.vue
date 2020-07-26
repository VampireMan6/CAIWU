<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container b-b">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<view class="w-100 f-between f-center m-b-60">
				<view>
					<text class="f-30 c-333 f-w-600">登录</text>
					<view class="relative">
						<view class="absolute view1 b-r-50"></view>
						<view class="absolute view2 b-r-50"></view>
					</view>
				</view>
				<view class="f-center" @tap="enter">
					<text class="f-15 c-333">去注册</text>
					<img class="enter-img m-l-10" src="../../static/tab-1/enter.png">
				</view>
			</view>
			<!-- 账号 -->
			<view class="w-100 f-between f-center m-b-10">
				<input type="number" class="w-78 f-20 c-333" v-model="phoneEmail1" maxlength="11" placeholder-style="f-15 c-999" :placeholder="placeholder1">
				<img @tap="delete1" v-if="phoneEmail1.length !==0 " class="delete-img" src="../../static/tab-1/delete1.png" alt="">
			</view>
			<!-- 密码 -->
			<view class="border-2 m-b-50" :class="phoneEmail1.length ==0 ? 'border-2' : 'border-22' "></view>
			<view class="w-100 f-between f-center m-b-10">
				<input type="text" :password="password" class="w-78 f-20 c-333" v-model="password1" placeholder-style="f-15 c-999" :placeholder="placeholder2">
				<img @tap="switchstate" v-if="password1.length !==0 " class="show-hidden" :src="'../../static/tab-1/attention'+forbid+'.png'"></img>
				<img @tap="delete2" v-if="password1.length !==0 " class="delete-img" src="../../static/tab-1/delete1.png" alt="">
			</view>
			<view class="border-2 m-b-30" :class="password1.length ==0 ? 'border-2' : 'border-22' "></view>
			<view class="w-100 f-end m-b-50" @tap="forgetPassword">
				<text class="f-15 c-666">忘记密码</text>
			</view>
			<!-- 登录 -->
			<view v-if="phoneEmail1.length !==0 && password1.length !==0" class="w-100 button2 f-center j-center m-b-50">
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
			forbid:"_forbid",
			password:true,
		}
	},
	methods: {
		delete1(){
			this.phoneEmail1 = "";
		},
		delete2(){
			this.password1 = "";
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
		enter(){//注册页面
			uni.navigateTo({
				url:'/pages/Login/SignIn'
			})
		},
		forgetPassword(){//忘记密码
			uni.navigateTo({
				url:'/pages/Login/ForgetPassword'
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
