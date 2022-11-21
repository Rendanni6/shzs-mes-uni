<template>
	<view class="wrap" style="padding-bottom: 60px;">
		<view>
			<u-form :model="form" class="apply-form-field">
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="布局地图" :border-bottom="false" style="font-size: 16px;" label-width="150" >
				</u-form-item>
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				
				<u-image src="/static/common/img/preventiveMeasureMap.jpg" width="100%" height="450px"></u-image>
				
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="防错点项" label-width="180" :label-style="{'font-size':'35rpx'}">
					<view solt="right" style="flex:1;text-align: right;align-items: center;color: blue;" @click="addunicollapseitem">
						添加
					</view>
					<view solt="right" style="margin-left:4px;color: blue;" @click="removeunicollapseitem">
						删除
					</view>
				</u-form-item>
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				
				<uni-collapse ref="collapse">
						<uni-collapse-item :title="item.head" v-for="(item, index) in itemList" :key="index" :open="item.open">
							<u-form-item label="防错点编号" class="marginLeft"  label-width="150" right-icon="arrow-right">
								<u-input placeholder="请选择" type="select" class="form-field-select"/>
							</u-form-item>
							
							<u-form-item label="设备编号"  class="marginLeft"  label-width="180">
								<u-input type="text" placeholder="请输入"/>
							</u-form-item>
							
							<u-form-item label="防错装置名称"  class="marginLeft"  label-width="180">
								<u-input type="text" placeholder="请输入"/>
							</u-form-item>
							
							<u-form-item label="验证频次" class="marginLeft"  label-width="150" right-icon="arrow-right">
								<u-input placeholder="请选择" type="select" class="form-field-select"/>
							</u-form-item>
							
							
							<u-form-item label="验证日期" class="marginLeft"  label-width="150" >
								<picker mode="date" style="margin-left: 93%;" :value="date" :start="startDate" :end="endDate" @change="bindDateChange(index,$event)">
										<view class="uni-input">{{item.date}}</view>
								</picker>
							</u-form-item>
							
							
							<u-form-item label="验证人" class="marginLeft"  label-width="150" right-icon="arrow-right">
								<u-input placeholder="请选择" type="select" class="form-field-select"/>
							</u-form-item>
							
							<u-form-item label="目前状态" class="marginLeft"  label-width="150" right-icon="arrow-right">
								<u-input placeholder="请选择" type="select" class="form-field-select"/>
							</u-form-item>
							
							<u-form-item label="下次验证日期" class="marginLeft"  label-width="180" >
								<picker mode="date" style="margin-left: 93%;" :value="nextDate" :start="startDate" :end="endDate" @change="bindNextDateChange(index,$event)">
										<view class="uni-input">{{item.nextDate}}</view>
								</picker>
							</u-form-item>
							
							<u-gap height="20" bg-color="#f5f5f5"></u-gap>
						</uni-collapse-item>
						
				</uni-collapse>
				
			</u-form>
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
			mode: 'date',
			date: currentDate,
			nextDate: currentDate,
			ishow: false,
			value: 0,
			      range: [
			        { value: 0, text: "日点检" },
			        { value: 1, text: "月点检" },
			        { value: 2, text: "年点检" },
			      ],	
			itemList: [{
							head: "防措点序号1",
							date: currentDate,
							nextDate: currentDate,
							open: false,
							disabled: true
						},
						{
							head: "防措点序号2",
							date: currentDate,
							nextDate: currentDate,
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
			}
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
			//点击添加增加折叠面板
			addunicollapseitem(){
				var len=this.itemList.length+1;
				this.itemList.push({'head':'防措点序号'+len,'open':true,'disabled':true});
				
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
			//绑定日期
			bindDateChange: function(index,e) {
				this.itemList[index].date=e.detail.value;
			},
			bindNextDateChange: function(index,e) {
				this.itemList[index].nextDate = e.detail.value;
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