<template>
	<view class="w-100 container b-b">
		<view class="w-100 column" v-for="(item,i) of list1" :key="i">
			<view class="f-between f-center m-b-10" @tap="enter(i)">
				<text class="f-15 c-333">{{item}}</text>
				<view v-if="i==0" class="f-15 c-999 f-center">
					<text v-if="mobile!==''">{{mobile}}</text>
					<view v-else class="f-center">
						<text>去绑定手机号</text>
						<img class="enter-img m-l-10" src="../../../static/tab-1/enter.png">
					</view>
				</view>
				<view v-if="i==1" class="f-15 c-999 f-center">
					<text v-if="mobile!==''">{{mobile}}</text>
					<view v-else class="f-center">
						<text>去绑定微信</text>
						<img class="enter-img m-l-10" src="../../../static/tab-1/enter.png">
					</view>
				</view>
				<view v-if="i==2" class="f-15 c-999 f-center">
					<text v-if="mobile!==''">{{mobile}}</text>
					<view v-else class="f-center">
						<text>去绑定邮箱</text>
						<img class="enter-img m-l-10" src="../../../static/tab-1/enter.png">
					</view>
				</view>
				<view v-if="i==3" class="f-15 c-999 f-center">
					<text v-if="mobile!==''">{{mobile}}</text>
					<view v-else class="f-center">
						<text>去修改密码</text>
						<img class="enter-img m-l-10" src="../../../static/tab-1/enter.png">
					</view>
				</view>
			</view>
			<view class="border-1 m-b-25"></view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 

export default {
	data() {
		return {
			list1:["手机号","微信","邮箱","账户密码"],
			mobile:"",
		}
	},
	methods: {
		enter(i){//绑定手机号
			if(i==0){
				uni.navigateTo({
					url:"/pages/Login/Binding-account"
				})
			}
			if(i==3){
				uni.navigateTo({
					url:"/pages/Login/ForgetPassword"
				})
			}
			
		}
	},
};
</script>

<style lang="scss">
	.container{
		padding: 50upx 40rpx;
		.enter-img{
			width:16upx;
			height: 24upx;
		}
	}
	
</style>
