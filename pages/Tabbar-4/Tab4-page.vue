<template>
	<view class="w-100 containers relative column">
		<!-- <view class="fixed nav"></view> -->
		<view class="container">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<!-- #ifdef APP-PLUS -->
			<view class="w-100 c-white f-17 p-15 b-b f-between f-center">
			<!-- #endif -->
			<!-- #ifdef H5 -->
			<view class="w-100 c-white f-17 p-x-15 p-t-30 b-b f-between f-center">
			<!-- #endif -->
				<text>上海惠满财科技有限公司</text>
				<!-- <img src="../../static" alt=""> -->
			</view>
		</view>
		<!-- 选项 -->
		<view class="w-100 p-x-15 b-b m-b-25 absolute select">
			<view class="nav-top b-c-w b-r-2 b-b f-13 c-333 w-100 f-between">
				<view class="f-center">
					<picker :range="arrays1" mode="multiSelector" @change="select1">
						<!-- <view class="">{{arrays1[arrayIndex1]}}</view> -->
						<view class="">{{  arrays1[0][arrayIndex1] }} - {{ arrays1[1][arrayIndex11]}}</view>
					</picker>
					<img @change="select1" class="img-select m-l-5" src="" alt="">
				</view>
				<view class="f-center">
					<picker :range="arrays2" mode="selector" @change="select2">
						<view class="">{{arrays2[arrayIndex2]}}</view>
					</picker>
					<img @change="select2" class="img-select m-l-5" src="" alt="">
				</view>
				<view class="f-center">
					<picker :range="arrays3" mode="selector" @change="select3">
						<view class="">{{arrays3[arrayIndex3]}}</view>
					</picker>
					<img @change="select3" class="img-select m-l-5" src="" alt="">
				</view>
			</view>
		</view>
		<!-- 水平滑动 -->
		<scroll-view class="scroll p-x-15 b-b m-t-40 column" scroll-x="true">
			<t-table>
				<t-tr v-if="show1">
					<t-td>
						<view class="t-td1 column f-center">
							<img @tap="enterTable" class="imgs" src="" alt="">
							<text @tap="enterTable" class="f-10 c-333 text1 b-b">图表</text>
						</view>
					</t-td>
					<t-td class="t-td2" v-for="(item,i) of datas1" :key="i">
						<text>{{item}}</text>
					</t-td>
				</t-tr>
				<t-tr v-else>
					<t-td class="t-td1 flex column f-center">
						<view class="t-td1 column f-center">
							<img @tap="enterChart" class="imgs" src="" alt="">
							<text @tap="enterChart" class="f-10 c-333 text1 b-b">表格</text>
						</view>
					</t-td>
					<t-td class="t-td2" v-for="(item2,j) of datas2" :key="j">
						<text>{{item2}}</text>
					</t-td>
				</t-tr>
			</t-table>
			<view v-show="show1" class="w-100 column">
				<!-- 1.规模 -->
				<view class="w-100 f-between">
					<text>1.规模</text>
					<text>(单位: 万元)</text>
				</view>
				<!-- 营业收入 -->
				<t-table>
					<t-tr>
						<t-td class="t-td1 flex column f-center">
							<text class="f-10 c-333 text1 b-b">营业收入</text>
						</t-td>
						<t-td class="t-td2" v-for="(item,i) of datas1" :key="i">{{item}}</t-td>
					</t-tr>
				</t-table>
				<!-- 净利润 -->
				<t-table>
					<t-tr>
						<t-td class="t-td1 flex column f-center">
							<text class="f-10 c-333 text1 b-b">净利润</text>
						</t-td>
						<t-td class="t-td2" v-for="(item,i) of datas1" :key="i">{{item}}</t-td>
					</t-tr>
				</t-table>
				<!-- 总资产 -->
				<t-table>
					<t-tr>
						<t-td class="t-td1 flex column f-center">
							<text class="f-10 c-333 text1 b-b">总资产</text>
						</t-td>
						<t-td class="t-td2" v-for="(item,i) of datas1" :key="i">{{item}}</t-td>
					</t-tr>
				</t-table>
				<!-- 2.成长性 -->
				<view class="w-100 f-between">
					<text>2.成长性</text>
				</view>
				<!-- 营业收入增长率 -->
				<t-table>
					<t-tr>
						<t-td class="t-td1 flex column f-center">
							<text class="f-10 c-333 text1 b-b">营业收入增长率</text>
						</t-td>
						<t-td class="t-td2" v-for="(item,i) of datas1" :key="i">{{item}}</t-td>
					</t-tr>
				</t-table>
				<!-- 净利润增长率 -->
				<t-table>
					<t-tr>
						<t-td class="t-td1 flex column f-center">
							<text class="f-10 c-333 text1 b-b">净利润增长率</text>
						</t-td>
						<t-td class="t-td2" v-for="(item,i) of datas1" :key="i">{{item}}</t-td>
					</t-tr>
				</t-table>
				<!-- 总资产增长率 -->
				<t-table>
					<t-tr>
						<t-td class="t-td1 flex column f-center">
							<text class="f-10 c-333 text1 b-b">总资产增长率</text>
						</t-td>
						<t-td class="t-td2" v-for="(item,i) of datas1" :key="i">{{item}}</t-td>
					</t-tr>
				</t-table>
				<!-- 2.成长性 -->
				<view class="w-100 f-between">
					<text>2.成长性</text>
				</view>
				<!-- 营业收入增长率 -->
				<t-table>
					<t-tr>
						<t-td class="t-td1 flex column f-center">
							<text class="f-10 c-333 text1 b-b">营业收入增长率</text>
						</t-td>
						<t-td class="t-td2" v-for="(item,i) of datas1" :key="i">{{item}}</t-td>
					</t-tr>
				</t-table>
				<!-- 净利润增长率 -->
				<t-table>
					<t-tr>
						<t-td class="t-td1 flex column f-center">
							<text class="f-10 c-333 text1 b-b">净利润增长率</text>
						</t-td>
						<t-td class="t-td2" v-for="(item,i) of datas1" :key="i">{{item}}</t-td>
					</t-tr>
				</t-table>
				<!-- 总资产增长率 -->
				<t-table>
					<t-tr>
						<t-td class="t-td1 flex column f-center">
							<text class="f-10 c-333 text1 b-b">总资产增长率</text>
						</t-td>
						<t-td class="t-td2" v-for="(item,i) of datas1" :key="i">{{item}}</t-td>
					</t-tr>
				</t-table>
			</view>
			<view v-show="show2">
				dfsadf
			</view>
		</scroll-view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 
import tTable from '@/components/t-table/t-table.vue';
import tTh from '@/components/t-table/t-th.vue';
import tTr from '@/components/t-table/t-tr.vue';
import tTd from '@/components/t-table/t-td.vue';

export default {
	data: function(){
		const date = new Date();
		const years1  = [];
		const years2  = [];
		for (let i = date.getFullYear()-1; i >= 1990; i--) {
			years1 .push(i)
		}
		for (let i = date.getFullYear(); i >= 1990; i--) {
			years2 .push(i)
		}
		return {
			// arrays1,
			years1,
			years2,
			arrays1:[
				years1,
				years2
			],
			arrays2:['第一季度','第二季度','第三季度','第四季度'],
			arrays3:['1月','2月','3月','4月','5月','6月','7月','8月','9月','10月','11月','12月'],
			arrayIndex1:0,
			arrayIndex11:0,
			arrayIndex2:0,
			arrayIndex3:0,
			datas1:[2016,2017,2018,2019,2020,2021,2022,2023,2024,2025],
			datas2:["规模","成长性","运营占比"],
			show1:true,
			show2:false
		}
	},
	components: {
	    tTable,
	    tTh,
	    tTr,
		tTd
	},
	methods: {
		select1(e){
			this.arrayIndex1 = e.detail.value[0];
			this.arrayIndex11 = e.detail.value[1];
		},
		select2(e){
			this.arrayIndex2 = e.detail.value;
		},
		select3(e){
			this.arrayIndex3 = e.detail.value;
		},
		enterTable(){
			this.show1 = false;
			this.show2 = true;
		},
		enterChart(){
			this.show2 = false;
			this.show1 = true;
		}
		
	},
	
};
</script>

<style lang="scss">
	.containers{
		.container{
			.status_bar {
			    height: var(--status-bar-height);
			    width: 100%;
			}
			height: 280upx;
			background-color: #000000;
		}
		.select{
			top: 210upx;
			z-index: 999;
			.nav-top{
				padding: 32upx 40upx;
				height: 100upx;
				box-shadow: 0upx 8upx 12upx 0 rgba(0, 0, 0, 0.1);
				.img-select{
					width: 18rpx;
					height: 24upx;
					background-color: #007AFF;
				}
			}
		}
		.scroll{
			.t-td1{
				.text1{
					width: 100upx;
				}
				.imgs{
					width: 20upx;
					height: 20upx;
					background-color: #007AFF;
				}
			}
		}
	}
	
</style>
