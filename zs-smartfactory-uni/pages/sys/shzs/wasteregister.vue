<template>
	<view class="wrap" style="padding-bottom: 60px;">
		<view>
			<u-form :model="form" class="apply-form-field">
				<u-form-item label="缺陷定位图" style="font-size: 16px;" label-width="180" >
				</u-form-item>
				<view  class="personnel-list">
					<view class="personnel-user">
						<image class="user-images" src="/static/aidex/images/add.jpg" @click=""></image>
						<!-- <i class="iconfont icon-close-circle-fill"></i> -->
						<view class="grid-text" style="text-align: center;">导入图片</view>
					</view>
				</view>	
				
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="基本信息" style="font-size: 16px;" label-width="150" >
				</u-form-item>
				
				<u-form-item label="产品类型" class="marginLeft" label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择产品类型" v-model="productionline" @click="show = true" type="select" class="form-field-select"/>
					<u-action-sheet :list="actionSheetList" v-model="show" @click="actionSheetCallback"></u-action-sheet>
				</u-form-item>
				<u-form-item label="工序" class="marginLeft"  label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择工序" type="select" class="form-field-select"/>
				</u-form-item>
				
				<u-form-item label="二维码" class="marginLeft" label-width="150" >
					<u-input placeholder="请扫描二维码"  type="text" input-align="right"/>
				</u-form-item>
				<u-form-item label="缺陷位置" class="marginLeft"  label-width="150" right-icon="arrow-right">
					<u-input placeholder="请在图上选择缺陷位置" type="select" class="form-field-select"/>
				</u-form-item>
				
				<u-form-item label="缺陷分类" class="marginLeft"  label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择缺陷分类" type="select" class="form-field-select"/>
				</u-form-item>
				<u-form-item label="缺陷名称" class="marginLeft"  label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择缺陷名称" type="select" class="form-field-select"/>
				</u-form-item>
				<u-form-item label="处理意见" class="marginLeft"  label-width="150" right-icon="arrow-right">
					<u-input placeholder="请输入处理意见" type="select" class="form-field-select"/>
				</u-form-item>
				
				
				<u-form-item label="缺陷图片"  label-width="250" :label-style="{'font-size':'20rpx'}">
				</u-form-item>
				<view  class="personnel-list">
					<view class="personnel-user">
						<image class="user-images" src="/static/aidex/images/add.jpg" @click=""></image>
						<!-- <i class="iconfont icon-close-circle-fill"></i> -->
						<view class="grid-text" style="text-align: center;">上传</view>
					</view>
				</view>	
				
			</u-form>
			<u-row gutter="32" class="bottom-box" justify="center">
				<u-col span="5">
					<view><u-button type="primary" shape="circle" @click="navTo('/pages/sys/msg/index')">提交</u-button></view>
				</u-col>
				<u-col span="5">
					<view><u-button shape="circle" @click="navTo('/pages/sys/home/index')">取消</u-button></view>
				</u-col>
			</u-row>
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
			productionline: '',
			actionSheetList: [
					{
						text: '巡检'
					},
					{
						text: '抽检'
					},
					{
						text: '全检'
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
		methods: {
			navTo(url) {
				uni.navigateTo({
					url: url
				});
			},
			// 点击actionSheet回调
			actionSheetCallback(index) {
				this.productionline = this.actionSheetList[index].text;
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