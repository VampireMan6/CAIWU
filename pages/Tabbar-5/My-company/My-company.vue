<template>
	<view class="companyList w-100 p-25 b-b column">
		<!-- 公司列表 -->
		<view class="w-100 column" v-for="(item,i) of datas1.data" :key="i">
			<view class="w-100 f-between f-center m-b-10">
				<view @tap="enter(i)" class="view-left">
					<img mode="aspectFill" class="w-100 h-100 b-r-2" :src="item.img" alt="">
				</view>
				<view class="view-right column">
					<view  @tap="enter(i)" class="view-top w-100">
						<text v-if="item.name.length<26" class="f-15 c-333">{{item.name}}</text>
						<text v-else class="f-15 c-333">{{item.name.slice(0,23)+'...'}}</text>
					</view>
					<view class="view-bottom w-100 f-between">
						<view  @tap="enter(i)" class="left h-100 f-10 c-999 f-center">
							<text>{{item.number}}</text>
							<text class="m-l-5">份历史财务数据</text>
						</view>
						<view class="right h-100 f-center j-center f-10 b-r-2">
							<text>+ 数据录入</text>
						</view>
					</view>
				</view>
			</view>
			<text class="f-10 c-999 m-b-10">上次录入数据：{{item.time}}</text>
			<view class="border-1 w-100 m-b-10"></view>
		</view>
		<view class="w-100 j-center m-b-15" @tap="addCompany">
			<text class="f-13 c-333 p-t-5 b-b">+ 新建公司</text>
		</view>
		<view class="border-1 w-100 p-x-25 b-b"></view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 
import companyList from '../../../static/json/Messagelist1.1.json'

export default {
	data() {
		return {
			datas1:companyList,
		}
	},
	methods: {
		enter(i){//修改公司信息页面
			let id = i;
			uni.navigateTo({
				url:('/pages/Tabbar-5/My-company/Change-company?id='+id)
			})
		},
		addCompany(){//新建公司
			uni.navigateTo({
				url:'/pages/Tabbar-5/My-company/Add-company'
			})
		}
	},
};
</script>

<style lang="scss">
	.companyList{
		.view-left{
			width: 200upx;
			height: 140upx;
		}
		.view-right{
			width: 416upx;
			height: 140upx;
			.view-top{
				height: 84upx;
			}
			.view-bottom{
				height: 48upx;
				.right{
					width: 134upx;
					color: #F54A35;
					background-color: rgba(245, 74, 53, 0.1);
				}
			}
		}
	}
	
</style>
