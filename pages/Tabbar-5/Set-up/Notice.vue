<template>
	<view class="w-100 container b-b">
		<view class="w-100 column">
			<view class="w-100 f-between f-center m-b-12">
				<text class="f-15 c-333">接收消息通知</text>
				<switch style="transform:scale(0.63)" :checked="true" @change="switch1" />
			</view>
			<view class="border-1 m-b-15"></view>
			<text class="f-12 c-999">打开后，不会错过最新活动和更多服务内容</text>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 

export default {
	data() {
		return {
			
		}
	},
	methods: {
		switch1(e){
			console.log(e.target.value)
		}
	},
};
</script>

<style lang="scss">
	.container{
		padding: 50upx 40rpx;
	}
	
</style>
