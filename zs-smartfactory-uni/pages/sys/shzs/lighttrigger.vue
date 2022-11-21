<template>
	<view class="wrap" style="padding-bottom: 60px;">
		<view>
			<u-form :model="form" class="apply-form-field">
				
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="当前按灯信息" style="font-size: 16px;" label-width="220" >
					<!-- <uni-icons style="margin-left: 98%;" custom-prefix="iconfontdo" type="icon-arrow-down" size="22" @click="formsitemshow"></uni-icons> -->
					<i class="iconfontdo icon-arrow-down"  style="font-size:22px;margin-left: 98%;"  v-show="iconDownShow" @click="formsitemshow"></i>	
					<i class="iconfontdo icon-arrow-right" style="font-size:22px;margin-left: 98%;"  v-show="iconRightShow" @click="formsitemshow"></i>	
					
					<!-- <uni-icons style="margin-left: 98%;" custom-prefix="arrow-down-font" type="icon-arrow-left" size="22"></uni-icons> -->
					
					<!-- <view solt="right" style="flex:1;text-align: right;align-items: center;color: blue;" @click="addunicollapseitem">
						添加
					</view>
					<view solt="right" style="margin-left:4px;color: blue;" @click="removeunicollapseitem">
						删除
					</view> -->
				</u-form-item>
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
					<uni-forms-item  v-for="(item, index) in itemList" :open="item.open" v-show="isShow">
					<u-form-item label="2020-08-02 16:28:54" style="font-size: 16px;" label-width="350" >
						<u-button v-if="item.status==1" solt="right" shape="square" :disabled="true" :hair-line="false" :plain="false"  style="margin-left: 32%;width: 80px;height: 25px;color: blue;">进行中</u-button>
						<u-button v-if="item.status==2" solt="right" shape="square" :disabled="true" :hair-line="false" :plain="false"  style="margin-left: 32%;width: 80px;height: 25px;color: blue;">等待中</u-button>
					</u-form-item>
					
					<u-form-item label="班次:" :border-bottom="false"  class="marginLeft" label-width="200" >
						<view solt="left" style="text-align:left;" >
							早班
						</view>
						<view  style="margin-left: 33%;text-align: right;" >
							报警级别:
						</view>
						<view  style="margin-left: 1%;text-align: right;" >
							四级报警
						</view>
					</u-form-item>
					
					<u-form-item label="工位/设备:" :border-bottom="false"  class="marginLeft" label-width="200" >
						<view solt="left" style="text-align:left;" >
							XXXXXXX
						</view>
						<view  style="margin-left: 30%;text-align: right;" >
							异常问题具体描述:
						</view>
						<view  style="margin-left: 1%;text-align: right;" >
							XXXXXXX
						</view>
					</u-form-item>
					
					<u-form-item label="操作工:"  :border-bottom="false" class="marginLeft" label-width="200" >
						<view solt="left" style="text-align:left;" >
							XXXXXXX
						</view>
						<view  style="margin-left: 30%;text-align: right;" >
							响应人:
						</view>
						<view  style="margin-left: 1%;text-align: right;" >
							李四
						</view>
					</u-form-item>
					
					<u-form-item label="问题分类:" :border-bottom="false"  class="marginLeft" label-width="200" >
						<view solt="left" style="text-align:left;" >
							XXXXXXX
						</view>
						<view  style="margin-left: 30%;text-align: right;" >
							响应时间:
						</view>
						<view  style="margin-left: 1%;text-align: right;" >
							2022-08-02 16:28:58
						</view>
					</u-form-item>
					
					<u-form-item label="具体类型:" :border-bottom="false" class="marginLeft" label-width="200" >
						<view solt="left" style="text-align:left;" >
							XXXXXXX
						</view>
						<view  style="margin-left: 30%;text-align: right;" >
							是否问题升级:
						</view>
						<view  style="margin-left: 1%;text-align: right;" >
							是
						</view>
					</u-form-item>
					<u-gap height="20" bg-color="#f5f5f5"></u-gap>	
					</uni-forms-item>
			</u-form>
		</view>
		
	</view>
</template>
<script>
export default {
		data() {
			return {
			val: '',
			maxLength:100,
			othersreson: '',
			maxLength:100,
			show: false,
			isShow: true,
			iconDownShow: true,
			iconRightShow: false,
			position: "right",
			value: 0,
			      range: [
			        { value: 0, text: "日点检" },
			        { value: 1, text: "月点检" },
			        { value: 2, text: "年点检" },
			      ],	
			itemList: [{
							status: "1",
							open: false,
							disabled: true
						},
						{
							status: "2",
							open: false,
							disabled: true
						}
						],
			status: 'loadmore',
			iconType: 'circle',
			isDot: false,
			loadText: {
						loadmore: '点击加载更多',
						loading: '正在加载...',
						nomore: '没有更多了'
			},
			}
		},
		computed:{
			remnant(){
				return this.val.length;
			}
		},
		created(){
		},
		onLoad() {
			
		},
		//新建按灯事件
		onNavigationBarButtonTap(e){
			this.itemList.push({'status':1,'disabled':true});
		},
		methods: {
			navTo(url) {
				uni.navigateTo({
					url: url
				});
			},
			// 点击actionSheet回调
			actionSheetCallback(index) {
				this.productionline = this.actionSheetList[index].text;
			},
			//点击添加增加折叠面板
			addunicollapseitem(){
				this.itemList.push({'status':1,'disabled':true});
				
			},
			//删除末尾折叠面板
			removeunicollapseitem(){
				var obj=this.itemList.pop();
				this.itemList.remove(obj);
			},
			//下拉框选项
			change(e){
				console.log(e);
			},
			//显示按灯信息
			formsitemshow(){
				this.isShow=!this.isShow;
				this.iconDownShow=!this.iconDownShow;
				this.iconRightShow=!this.iconRightShow;
			},
			//点击图标事件
			clickRight(){
				alert(123456);
			}
		}

	}
</script>
<style lang="scss" scoped>
@import 'index.scss';
page {
	background-color: #f5f5f5;
}
.wrap .search{
	background: #ffffff;
}
.apply-text{
	font-size: 28rpx;
	color: #333333;
	span{
		color: #999999;
	}
}
.marginLeft{
	margin-left: 20px;
}

.apply-list-foot{
	font-size: 28rpx;
}

.parents{
	width: 100%;
	height: 80%;
	position: relative;
}

.personnel-list{
	display: flex;
	align-items: center;
	flex-wrap:wrap;
	.personnel-user{
		position: relative;
		margin: 5px 9px 0;
	}
	.user-images{
		width: 48px;
		height:48px;
		margin-right:0;
		
	}
	.iconfont{
		position: absolute;
		top:-12px;
		right:-5px;
		color: #FE0100;
	}
	
}
</style>