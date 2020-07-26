<template>
	<view class="container column w-100 b-b">
		<text class="f-13 c-333 m-b-15">我的昵称 :</text>
		<view class="w-100 b-c-f8 j-center f-center input m-b-50 b-r-2">
			<input type="text" class="b-c-f8   f-15 c-333" v-model="name" placeholder-style="f-15 c-999" :placeholder="placeholder">
		</view>
		<view class="w-100 j-center true">
			<text class="f-15 c-white text b-b b-r-2">确定</text>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 

export default {
	data() {
		return {
			placeholder:"用户昵称",
			name:""
		}
	},
	methods: {
		
	},
};
</script>

<style lang="scss">
	.container{
		padding: 80upx 76upx;
		.input{
			height: 100upx;
		}
		.true{
			.text{
				background-color: #F54A35;
				padding: 20upx 90upx;
			}
		}
	}
	
</style>
