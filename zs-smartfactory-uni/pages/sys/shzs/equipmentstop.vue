<template>
	<view class="wrap" style="padding-bottom: 60px;">
		<view>
			<u-form :model="form" class="apply-form-field">
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="基本信息" style="font-size: 16px;" label-width="150" >
				</u-form-item>
				<u-form-item label="设备名称" class="marginLeft" label-width="150" >
					<u-input :disabled="true" value="GMS0001" type="text" input-align="right"/>
				</u-form-item>
				
				<u-form-item label="设备编号" class="marginLeft" label-width="150" >
					<u-input :disabled="true" value="SVN0001" type="text" input-align="right"/>
				</u-form-item>
				
				<u-form-item label="汇报人" class="marginLeft" label-width="150" >
					<u-input :disabled="true" value="张三" type="text" input-align="right"/>
				</u-form-item>
				
				<u-form-item label="停机开始时间" class="marginLeft" label-width="180" >
					<!-- <u-input placeholder="请输入" type="text" input-align="right"/> -->
					<picker  mode="date" style="margin-left: 93%;" :value="shutdownDate" :start="startDate" :end="endDate" @change="bindDateChange(1,$event)">
							<view class="uni-input" >{{shutdownDate}}</view>
					</picker>
				</u-form-item>
				
				<u-form-item label="停机结束时间" class="marginLeft" label-width="180" >
					<!-- <u-input  placeholder="请输入" type="text" input-align="right"/> -->
					<picker mode="date" style="margin-left: 93%;" :value="shutdownEndDate" :start="startDate" :end="endDate" @change="bindDateChange(2,$event)">
							<view class="uni-input">{{shutdownEndDate}}</view>
					</picker>
				</u-form-item>
				
				
				<u-form-item label="停机类型" class="marginLeft" label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择" v-model="productionline" @click="show = true" type="select" class="form-field-select"/>
					<u-action-sheet :list="actionSheetList" v-model="show" @click="actionSheetCallback"></u-action-sheet>
				</u-form-item>
				
				<u-form-item label="是否按灯" class="marginLeft" label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择" type="select" class="form-field-select"/>
				</u-form-item>
				
				<u-form-item label="是否升级" class="marginLeft" label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择" type="select" class="form-field-select"/>
				</u-form-item>
				
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="停机说明"  label-width="180" :label-style="{'font-size':'20rpx'}">
					<view solt="right" style="flex:1;text-align: right;align-items: center;">
					</view>
				</u-form-item>
				<p class="wrap">
					<p class="parents">
						<u-form-item><u-input type="textarea" style="background-color:whitesmoke;" placeholder="请输入详细的情况说明" autofocus="true" v-model="val"  maxlength="100"/></u-form-item>
						<span class="tips">
							<b :class="{'remnant':remnant.length!=0,'zero':remnant.length==0}">{{remnant}}/100</b>
						</span>
					</p>
				</p>
				<u-form-item label="检验结果"  label-width="250" :label-style="{'font-size':'20rpx'}">
				</u-form-item>
				<u-form-item >
					<view><u-button size="medium"  @click="navTo('/pages/sys/msg/index')">合格</u-button></view>
					<view><u-button style="margin-left: 25px;" size="medium" type="default" @click="navTo('/pages/sys/msg/index')">不合格</u-button></view>
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
			const currentDate = this.getDate({
			            format: true
			        });
			return {
			val: '',
			maxLength:100,
			othersreson: '',
			maxLength:100,
			show: false,
			productionline: '',
			actionSheetList: [
					{
						text: '重启'
					},
					{
						text: '暂时'
					},
					{
						text: '永久'
					}
				],
			shutdownDate: currentDate,
			shutdownEndDate: currentDate,
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
			},
			startDate() {
			    return this.getDate('start');
			},
			endDate() {
				return this.getDate('end');
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
			//绑定日期
			bindDateChange: function(index,e) {
				debugger;
				if(index==1){
					this.shutdownDate=e.detail.value;
				}else{
					this.shutdownEndDate=e.detail.value;
				}
			},
			//获取日期
			getDate(type) {
				const date = new Date();
				let year = date.getFullYear();
				let month = date.getMonth() + 1;
				let day = date.getDate();
				
				if (type === 'start') {
					year = year - 60;
				} else if (type === 'end') {
					year = year + 5;
				}
				month = month > 9 ? month : '0' + month;
				day = day > 9 ? day : '0' + day;
				return `${year}-${month}-${day}`;
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
