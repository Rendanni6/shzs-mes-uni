<template>
	<view class="wrap" style="padding-bottom: 60px;">
		<view>
			<u-form :model="form" class="apply-form-field">
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="基本信息" style="font-size: 16px;" label-width="150" >
				</u-form-item>
				
				<u-form-item label="检验类型" class="marginLeft" label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择" v-model="productionline" @click="show = true" type="select" class="form-field-select"/>
					<u-action-sheet :list="actionSheetList" v-model="show" @click="actionSheetCallback"></u-action-sheet>
				</u-form-item>
				
				<!-- <u-gap height="20" bg-color="#f5f5f5"></u-gap> -->
				<u-form-item label="检验员" class="marginLeft" label-width="150" >
					<u-input placeholder="请输入" value="xxxx有限公司"  type="text" input-align="right"/>
				</u-form-item>
				<u-form-item label="产线" class="marginLeft"  label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择" type="select" class="form-field-select"/>
				</u-form-item>
				<u-form-item label="制程" class="marginLeft"  label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择" type="select" class="form-field-select"/>
				</u-form-item>
				<u-form-item label="设备" class="marginLeft"  label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择" type="select" class="form-field-select"/>
				</u-form-item>
				
				
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="检查项目" label-width="180" :label-style="{'font-size':'35rpx'}">
					<view solt="right" @click="addProcessItemList" style="flex:1;text-align: right;align-items: center;color: blue;">
						添加
					</view>
				</u-form-item>
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				
				<uni-collapse ref="collapse">
						<uni-collapse-item :title="item.head" v-for="(item, index) in itemList" :open="item.open">
							
							<u-form-item label="检查项目" class="marginLeft"  label-width="150" right-icon="arrow-right">
								<u-input placeholder="请选择" type="select" class="form-field-select"/>
							</u-form-item>
							
							<u-form-item label="检查内容"  class="marginLeft"  label-width="180">
								<u-input type="text" placeholder="请输入"/>
							</u-form-item>
							
							<u-form-item label="检查值"  class="marginLeft"  label-width="180">
								<u-input type="text" placeholder="请输入"/>
							</u-form-item>
							
							<u-form-item label="检查结果" class="marginLeft"  label-width="150" right-icon="arrow-right">
								<u-input placeholder="请选择" type="select" class="form-field-select"/>
							</u-form-item>
							
							<u-gap height="20" bg-color="#f5f5f5"></u-gap>
						</uni-collapse-item>
				</uni-collapse>
				
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="检查结果" label-width="180" :label-style="{'font-size':'35rpx'}">
					<view solt="right" style="flex:1;text-align: right;align-items: center;">
					</view>
				</u-form-item>
				
				<u-form-item label="检验单"  label-width="250" :label-style="{'font-size':'20rpx'}">
				</u-form-item>
				<view  class="personnel-list">
					<view class="personnel-user">
						<image class="user-images" src="/static/aidex/images/add.jpg" @click=""></image>
						<!-- <i class="iconfont icon-close-circle-fill"></i> -->
						<view class="grid-text" style="text-align: center;">上传</view>
					</view>
				</view>	
				<u-form-item label="处理对策"  label-width="250" :label-style="{'font-size':'20rpx'}">
				</u-form-item>
				<u-form-item >
					<view><u-button size="medium" @click="navTo('/pages/sys/msg/index')">继续作业</u-button></view>
					<view><u-button style="margin-left: 25px;" size="medium" type="default" @click="navTo('/pages/sys/msg/index')">停线检修</u-button></view>
				</u-form-item>
				
			</u-form>
			<u-row gutter="32" class="bottom-box" justify="center">
				<u-col span="5">
					<view><u-button type="primary" shape="circle" @click="navTo('/pages/sys/msg/index')">确定</u-button></view>
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
			itemList: [{
							head: "检验项次1",
							body: "只要我们正确择取一个合适的参照物乃至稍降一格去看待他人，值得赏识的东西便会扑面而来",
							open: true,
							disabled: true
						}],
			
			
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
			},
			//添加
			addProcessItemList(){
				var len=this.itemList.length+1;
				this.itemList.push({'head':'检查项次'+len,'open':true,'disabled':true});
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