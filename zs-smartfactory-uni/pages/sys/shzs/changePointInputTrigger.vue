<template>
	<view class="wrap" style="padding-bottom: 60px;">
		<view>
			<u-form :model="form" class="apply-form-field">
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="基本信息" :border-bottom="false" style="font-size: 16px;" label-width="150" >
				</u-form-item>
				
				<u-form-item label="产线" class="marginLeft" label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择" type="select" class="form-field-select"/>
				</u-form-item>
				
				<u-form-item label="工位/设备" class="marginLeft" label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择" type="select" class="form-field-select"/>
				</u-form-item>
				
				<u-form-item label="变化点识别人员" class="marginLeft" label-width="220" >
					<u-input placeholder="请输入" type="text" class="form-field-select"/>
				</u-form-item>
				
				<u-form-item label="变化开始前二维码"  class="marginLeft"  label-width="250">
					<u-input type="text" value="xxxx"/>
				</u-form-item>
				
				<u-form-item label="变化类型" class="marginLeft" label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择" type="select" class="form-field-select"/>
				</u-form-item>
				
				<u-form-item label="变化点" class="marginLeft" label-width="150" right-icon="arrow-right">
					<u-input placeholder="请选择" type="select" class="form-field-select"/>
				</u-form-item>
				
				<u-form-item label="变化点具体描述"  class="marginLeft"  label-width="250">
					<u-input type="text" placeholder="请输入"/>
				</u-form-item>
				
				<u-form-item label="变化点是否触发快反" class="marginLeft" label-width="280" right-icon="arrow-right">
					<u-input placeholder="请选择" type="select" class="form-field-select"/>
				</u-form-item>
				
				<!-- <u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="检验项目" label-width="180" :label-style="{'font-size':'35rpx'}">
					<view solt="right" style="flex:1;text-align: right;align-items: center;color: blue;" @click="addunicollapseitem">
						添加
					</view>
					<view solt="right" style="margin-left:4px;color: blue;" @click="removeunicollapseitem">
						删除
					</view>
				</u-form-item>
				<u-gap height="20" bg-color="#f5f5f5"></u-gap> -->
				
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="变化点控制措施" :border-bottom="false" style="font-size: 16px;" label-width="250" >
				</u-form-item>
				<uni-collapse ref="collapse" v-for="(item, index) in itemList">
						<u-icon class="collapseItemlistIcon" size="40" :name="item.imageFlag==true?item.checked:item.check" @click="changeImage(index,$event)"></u-icon>
						
						<uni-collapse-item class="collapseItemlist"  :title="item.head" :open="item.open" :disabled="item.disabled" :show-arrow="item.showArrow">
							<u-form-item label="责任人" class="marginLeft"  label-width="150" right-icon="arrow-right">
								<u-input placeholder="请选择" type="select" class="form-field-select"/>
							</u-form-item>
							
							<u-form-item label="执行周期"  class="marginLeft"  label-width="180">
								<u-input placeholder="请选择" type="select" class="form-field-select"/>
							</u-form-item>
							
							<u-form-item label="防错清单"  class="marginLeft"  label-width="180">
								<u-input placeholder="请选择" type="select" class="form-field-select"/>
							</u-form-item>
							
							<u-gap height="20" bg-color="#f5f5f5"></u-gap>
						</uni-collapse-item>
				</uni-collapse>
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
			value: 0,
			      range: [
			        { value: 0, text: "日点检" },
			        { value: 1, text: "月点检" },
			        { value: 2, text: "年点检" },
			      ],	
			itemList: [{
							head: "班组安全培训",
							check: "/static/common/img/checkbox-fill.png",
							checked: "/static/common/img/checkedbox-fill.png",
							imageFlag: false,
							showArrow: false,
							open: false,
							disabled: true
						},
						{
							head: "带教师傅岗位带教",
							check: "/static/common/img/checkbox-fill.png",
							checked: "/static/common/img/checkedbox-fill.png",
							imageFlag: false,
							showArrow: false,
							open: false,
							disabled: true
						},
						{
							head: "员工操作当班首件质量抽检",
							check: "/static/common/img/checkbox-fill.png",
							checked: "/static/common/img/checkedbox-fill.png",
							imageFlag: false,
							showArrow: false,
							open: false,
							disabled: true
						},
						{
							head: "员工操作当班中件质量抽检",
							check: "/static/common/img/checkbox-fill.png",
							checked: "/static/common/img/checkedbox-fill.png",
							imageFlag: false,
							showArrow: false,
							open: false,
							disabled: true
						},
						{
							head: "班组安全培训",
							check: "/static/common/img/checkbox-fill.png",
							checked: "/static/common/img/checkedbox-fill.png",
							imageFlag: false,
							showArrow: false,
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
				this.itemList.push({'head':'点检序号'+len,'open':true,'disabled':true});
				
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
			//切换图标
			changeImage(index,event){
				this.itemList[index].imageFlag=!this.itemList[index].imageFlag;
				this.itemList[index].showArrow=!this.itemList[index].showArrow;
				this.itemList[index].disabled=!this.itemList[index].disabled;
				if(this.itemList[index].imageFlag == false){
					this.itemList[index].open = false
				}
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

.collapseItemlistIcon{
	position: absolute;
	margin-top: 12px;
}

.collapseItemlist{
	margin-left: 12px;
}

</style>
