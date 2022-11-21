<template>
	<view class="wrap" style="padding-bottom: 60px;">
		<view>
			<u-form :model="form" class="apply-form-field">
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="基本信息" :border-bottom="false" style="font-size: 16px;" label-width="150" >
				</u-form-item>
				
				<u-form-item label="设备名称" class="marginLeft" label-width="150" >
					<u-input value="GMS001"  type="text" input-align="right"/>
				</u-form-item>
				
				<u-form-item label="设备编号" class="marginLeft" label-width="150" >
					<u-input  value="xxxx有限公司"  type="text" input-align="right"/>
				</u-form-item>
				
				<u-form-item label="点检类型" class="marginLeft" label-width="150" >
					<!-- <u-input placeholder="请选择" v-model="productionline" @click="show = true" type="select" class="form-field-select"/> -->
					<!-- <u-action-sheet :list="actionSheetList" v-model="show" @click="actionSheetCallback"></u-action-sheet> -->
						<uni-data-select style="margin-left: 90%;"
						      v-model="value"
						      :localdata="range"
						      @change="change"
							  :clear="false"
						    ></uni-data-select>
						</uni-section>
				</u-form-item>
				
				<u-form-item label="执行人"  class="marginLeft"  label-width="180">
					<u-input type="text" placeholder="请输入"/>
				</u-form-item>
				
				<u-form-item label="执行时间"  class="marginLeft"  label-width="180">
					<u-input type="text" placeholder="请输入"/>
				</u-form-item>
				
				
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="检验项目" label-width="180" :label-style="{'font-size':'35rpx'}">
					<view solt="right" style="flex:1;text-align: right;align-items: center;color: blue;" @click="addunicollapseitem">
						添加
					</view>
					<view solt="right" style="margin-left:4px;color: blue;" @click="removeunicollapseitem">
						删除
					</view>
				</u-form-item>
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				
				<uni-collapse ref="collapse">
					<!-- <i class="iconfontdo icon-arrow-down"  style="font-size:22px;margin-left: 98%;"  v-show="iconDownShow" @click="formsitemshow"></i>	 -->
						<uni-collapse-item :title="item.head" v-for="(item, index) in itemList" :open="item.open" :show-arrow="true" >
							<!-- {{item.body}} -->
							<u-form-item label="点检项" class="marginLeft"  label-width="150" right-icon="arrow-right">
								<u-input placeholder="请选择" type="select" class="form-field-select"/>
							</u-form-item>
							
							<u-form-item label="点检内容"  class="marginLeft"  label-width="180">
								<u-input type="text" placeholder="请输入"/>
							</u-form-item>
							
							<u-form-item label="点检方式"  class="marginLeft"  label-width="180">
								<u-input type="text" placeholder="请输入"/>
							</u-form-item>
							
							<u-form-item label="点检结果" class="marginLeft"  label-width="150" right-icon="arrow-right">
								<u-input placeholder="请选择" type="select" class="form-field-select"/>
							</u-form-item>
							
							<u-form-item  label="附件"  :border-bottom="false" class="marginLeft" label-width="150" :label-style="{'font-size':'20rpx'}">
							</u-form-item>
								
							<u-upload ref="uUpload" class="marginLeft" :action="action" :auto-upload="false" ></u-upload>
							<u-gap height="20" bg-color="#f5f5f5"></u-gap>
						</uni-collapse-item>
				</uni-collapse>
				
				
				<u-gap height="20" bg-color="#f5f5f5"></u-gap>
				<u-form-item label="检验结果"  :border-bottom="false" label-width="250" :label-style="{'font-size':'20rpx'}">
				</u-form-item>
				<u-form-item >
					<view><u-button size="medium" type="primary"  @click="">合格</u-button></view>
					<view><u-button style="margin-left: 25px;" size="medium" type="default" @click="">不合格</u-button></view>
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
			value: 0,
			      range: [
			        { value: 0, text: "日点检" },
			        { value: 1, text: "月点检" },
			        { value: 2, text: "年点检" },
			      ],	
			itemList: [{
							head: "点检序号1",
							open: false,
							disabled: true
						},
						{
							head: "点检序号2",
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
