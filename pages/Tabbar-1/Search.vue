<template>
	<view class="w-100 containers column">
		<view class="fixed nav"></view>
		<view class="container p-t-10 b-b p-x-15">
			<!-- 顶部占位符 -->
			<view class="w-100 status_bar"></view>
			<!-- 搜索 -->
			<mSearch class="mSearch-input-box w-100 m-b-20"
			:mode="1" button="outside" 
			:placeholder="defaultKeyword"
			@search="doSearch(false)" 
			@input="inputChange" 
			@confirm="doSearch(false)" 
			v-model="keyword"></mSearch>
			<!-- 历史搜索 -->
			<view class="w-100 history-search p-x-15 b-b" @touchstart="blur">
				<view class="w-100 column" v-show="isShowKeywordList" v-if="oldKeywordList.length>0">
					<view class="nav-top w-100 f-between f-center m-b-15">
						<text class="f-15 c-999">历史搜索</text>
						<image @tap="oldDelete" class="delete-img" src="../../static/tab-1/delete.png"></image>
					</view>
					<view class="w-100 f-w">
						<view v-for="(keyword,index) in oldKeywordList" @tap="doSearch(keyword)" :key="index">
							<text class="f-12 c-333 p-10 b-b b-c-f8 m-r-15 m-b-15 b-r-2">{{keyword}}</text>
						</view>
					</view>
					<view class="border-1 m-b-20"></view>
				</view>
			</view>
			<!-- 热门搜索 -->
			<view class="w-100 keyword-block p-x-15 b-b column" v-show="isShowKeywordList">
				<view class="w-100 f-between f-center m-b-15">
					<view class="f-15 c-999">热门搜索</view>
					<image @tap="hotToggle" class="attention-img" :src="'../../static/tab-1/attention'+forbid+'.png'"></image>
				</view>
				<view class="w-100 f-w" v-if="forbid==''">
					<view v-for="(keyword,index) in hotKeywordList" @tap="doSearch(keyword)" :key="index">
						<text class="f-12 c-333 p-10 b-b b-c-f8 m-r-15 m-b-15 b-r-2">{{keyword}}</text>
					</view>
				</view>
				<view class="w-100 j-center" v-else>
					<view class="f-10 c-999">当前搜热门搜索已隐藏</view>
				</view>
			</view>
			<!-- 公司列表 -->
			<view v-show="show" class="companyList w-100 p-x-15 b-b column">
				<view class="w-100 column" v-for="(item,i) of datas1.data" :key="i">
					<view class="w-100 m-b-25 f-between f-center">
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
									<text>+ 公司对比</text>
								</view>
							</view>
						</view>
					</view>
					<view class="border-1 w-100 m-b-25"></view>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	
// import util from '../../common/util.js'; 
import mSearch from '@/components/mehaotian-search-revision/mehaotian-search-revision.vue';
import companyList from '../../static/json/Messagelist1.json'

export default {
	onLoad() {
		this.init();
	},
	data() {
		return {
			datas1:companyList,
			defaultKeyword: "",
			keyword: "",
			oldKeywordList: [],
			hotKeywordList: [],
			keywordList: [],
			forbid: '',
			isShowKeywordList: true,
			show: false,
		}
	},
	components: {
		mSearch,
	},
	methods: {
		init() {
			this.loadDefaultKeyword();
			this.loadOldKeyword();
			this.loadHotKeyword();
		},
		blur(){
			uni.hideKeyboard()
		},
		//加载默认搜索关键字
		loadDefaultKeyword() {
			//定义默认搜索关键字，可以自己实现ajax请求数据再赋值,用户未输入时，以水印方式显示在输入框，直接不输入内容搜索会搜索默认关键字
			this.defaultKeyword = "请输入搜索内容";
		},
		//加载历史搜索,自动读取本地Storage
		loadOldKeyword() {
			uni.getStorage({
				key: 'OldKeys',
				success: (res) => {
					// console.log(res);
					var OldKeys = JSON.parse(res.data);
					this.oldKeywordList = OldKeys;
				}
			});
		},
		//加载热门搜索
		loadHotKeyword() {
			//定义热门搜索关键字，可以自己实现ajax请求数据再赋值
			this.hotKeywordList = ['埋线双眼皮', '下睑下至术', '切开双眼皮', '开内眼角', '内切去眼袋', '切眉术', '上眼提肌', '去黑眼圈', '水光针', '牙齿美容', '光子嫩肤'];
		}, 
		//监听输入
		inputChange(event) {
			this.isShowKeywordList = true;
			this.show = false
		},
		//高亮关键字
		drawCorrelativeKeyword(keywords, keyword) {
			var len = keywords.length,
				keywordArr = [];
			for (var i = 0; i < len; i++) {
				var row = keywords[i];
				//定义高亮#9f9f9f
				var html = row[0].replace(keyword, "<span style='color: #9f9f9f;'>" + keyword + "</span>");
				html = '<div>' + html + '</div>';
				var tmpObj = {
					keyword: row[0],
					htmlStr: html
				};
				keywordArr.push(tmpObj)
			}
			return keywordArr;
		},
		//顶置关键字
		setkeyword(data) {
			this.keyword = data.keyword;
		},
		//清除历史搜索
		oldDelete() {
			uni.showModal({
				content: '确定清除历史搜索记录？',
				success: (res) => {
					if (res.confirm) {
						this.oldKeywordList = [];
						uni.removeStorage({
							key: 'OldKeys'
						});
					} else if (res.cancel) {
						
					}
				}
			});
		},
		// //热门搜索开关
		hotToggle() {
			this.forbid = this.forbid ? '' : '_forbid';
		},
		//执行搜索
		doSearch(key) {
			this.show=!this.show;
			this.isShowKeywordList=!this.isShowKeywordList;
			key = key ? key : this.keyword ? this.keyword : this.defaultKeyword;
			this.keyword = key;
			this.saveKeyword(key); //保存为历史 
			
		},
		//保存关键字到历史记录
		saveKeyword(keyword) {
			uni.getStorage({
				key: 'OldKeys',
				success: (res) => {
					// console.log(res.data);
					var OldKeys = JSON.parse(res.data);
					var findIndex = OldKeys.indexOf(keyword);
					if (findIndex == -1) {
						OldKeys.unshift(keyword);
					} else {
						OldKeys.splice(findIndex, 1);
						OldKeys.unshift(keyword);
					}
					//最多10个纪录
					OldKeys.length > 10 && OldKeys.pop();
					uni.setStorage({
						key: 'OldKeys',
						data: JSON.stringify(OldKeys)
					});
					this.oldKeywordList = OldKeys; //更新历史搜索
				},
				fail: (e) => {
					var OldKeys = [keyword];
					uni.setStorage({
						key: 'OldKeys',
						data: JSON.stringify(OldKeys)
					});
					this.oldKeywordList = OldKeys; //更新历史搜索
				}
			})
		},
		enter(i){
			let id = i;
			uni.navigateTo({
				url:('/pages/Tabbar-2/Company-message?id='+id)
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
			.status_bar {
			     height: var(--status-bar-height);
			     width: 100%;
			}
			.mSearch-input-box{
				height: 60upx;
			}
			.history-search{
				.nav-top{
					.delete-img{
						width: 40rpx;
						height: 40upx;
					}
				}
			}
			.keyword-block{
				.attention-img{
					width: 40rpx;
					height: 40upx;
				}
			}
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
		}
	}
	
</style>
