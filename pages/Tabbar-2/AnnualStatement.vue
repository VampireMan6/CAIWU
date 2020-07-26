<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container p-15 b-b">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<view class="w-100 nav-b f-between">
				<img class="return-img" src="../../static/tab-2/return-b.png" alt="" @click="back">
				<text>{{datas2[id]}} 年度数据</text>
				<img class="share-img" src="../../static/tab-2/share-b.png" alt="">
			</view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 

export default {
	onLoad(option) {
		if(option.id !==undefined){
			this.id = option.id;
		}
	},
	data() {
		return {
			id:0,
			datas2:[2019,2018,2017],
		}
	},
	methods: {
		back(){
			uni.navigateBack({})
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
			.nav-b{
				.return-img,.share-img{
					width:44upx;
					height: 44upx;	
				}
			}
		}
	}
</style>
