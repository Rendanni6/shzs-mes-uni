<template>
	<view class="wrap" style="padding-bottom: 60px;">
		<view>
			<u-form :model="form" class="apply-form-field">
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="基本信息" style="font-size: 16px;" label-width="150" >
				</u-form-item>
				<u-form-item label="产线" class="marginLeft" label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择" type="select" class="form-field-select"/>
				</u-form-item>
				<!-- <u-gap height="20" bg-color="#f5f5f5"></u-gap> -->
				<u-form-item label="班组长" class="marginLeft" label-width="150" >
					<u-input value="赵老六" type="text" input-align="right"/>
				</u-form-item>
				<u-form-item label="产品型号" class="marginLeft"  label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择" type="select" class="form-field-select"/>
				</u-form-item>
				<!-- <u-gap height="20" bg-color="#f5f5f5"></u-gap> -->
				<u-form-item label="当班计划产量"  class="marginLeft"  label-width="180">
					<u-input type="text" placeholder="请输入"/>
				</u-form-item>
				
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="录入人员" label-width="180" :label-style="{'font-size':'35rpx'}">
					<view solt="right" style="flex:1;text-align: right;align-items: center;">
					</view>
				</u-form-item>
				<u-form-item label="当班人员"  label-width="150">
					<view solt="right" style="flex:1;text-align: right;align-items: center;">
					</view>
				</u-form-item>
				<u-form-item>
					<view  class="personnel-list">
						<view class="personnel-user">
							<image class="user-images" src="/static/aidex/images/add.jpg"></image>
							<i class="iconfont icon-close-circle-fill"></i>
							<view class="grid-text" style="text-align: center;">添加</view>
						</view>
						<view class="personnel-user">
							<image class="user-images" src="/static/aidex/images/user01.png"></image>
							<i class="iconfont icon-close-circle-fill"></i>
							<view class="grid-text" style="text-align: center;">张三</view>
						</view>
						<view class="personnel-user">
							<image class="user-images" src="/static/aidex/images/user02.png"></image>
							<i class="iconfont icon-close-circle-fill"></i>
							<view class="grid-text" style="text-align: center;">李四</view>
						</view>
						<view class="personnel-user">
							<image class="user-images" src="/static/aidex/images/user03.png"></image>
							<i class="iconfont icon-close-circle-fill"></i>
							<view class="grid-text" style="text-align: center;">王老五</view>
						</view>
						<view class="personnel-user">
							<image class="user-images" src="/static/aidex/images/user04.png"></image>
							<i class="iconfont icon-close-circle-fill"></i>
							<view class="grid-text" style="text-align: center;">赵麻子</view>
						</view>
						<view class="personnel-user">
							<image class="user-images" src="/static/aidex/images/user05.png"></image>
							<i class="iconfont icon-close-circle-fill"></i>
							<view class="grid-text" style="text-align: center;">周瑜黄盖</view>
						</view>
					</view>
				</u-form-item>
				<u-form-item label="上班情况说明"  label-width="180" :label-style="{'font-size':'20rpx'}">
					<view solt="right" style="flex:1;text-align: right;align-items: center;">
					</view>
				</u-form-item>
				<p class="wrap">
					<p class="parents">
						<u-form-item><u-input type="textarea"  placeholder="请输入详细的情况说明" autofocus="true" v-model="val"  maxlength="100"/></u-form-item>
						<span class="tips">
							<b :class="{'remnant':remnant.length!=0,'zero':remnant.length==0}">{{remnant}}/100</b>
						</span>
					</p>
				</p>
			</u-form>
			<u-row gutter="32" class="bottom-box" justify="center">
				<u-col span="5">
					<view><u-button type="primary" shape="circle" @click="navTo('/pages/sys/msg/index')">开始上班</u-button></view>
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
			show: false,
			val: '',
			maxLength:100,
			m2mSimflowList:[],
			m2mOrderFlowList:[],
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
			// uni.setNavigationBarTitle({
			// 	title: '班组交接'
			// });
		},
		methods: {
			navTo(url) {
				console.log(123+"====>"+url);
				uni.navigateTo({
					url: url
				});
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

.user-images{
	width: 28px;
	height:28px;
	margin-right: 8px;
}
.apply-list-foot{
	font-size: 28rpx;
}

.parents{
	width: 100%;
	height: 80%;
	position: relative;
}

textarea{
	position: absolute;
	left: 0;
	right: 0;
	width: 100%;
	height: 100%;
}

.tips{
	position: absolute;
	bottom: 0;
	right: 0;
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
