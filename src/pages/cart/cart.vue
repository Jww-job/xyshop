<template>
	<view class="cart">
		<!-- 头部 -->
		<view class="cart-top">
			<view class="count-box" style="color: #999;">		
			</view>
			<view >
				<view class="cu-btn set-btn sm round" @tap="deleteGoods"><text class="cuIcon-delete"></text>删除</view>
			</view>
		</view>
		
		<!-- 内容部分 -->
		<scroll-view 
		class="cart-scroll"
		@scroll="Scroll"
		id="1"
		scroll-y="true"
		:scroll-top="scrollTop"
		ower-threshold="100"
		scroll-with-animation="200">
		<view class="cart-content">
			<view v-for="(item,index) in lists" :key="index" class="cart-item bg-white">
				
				<view class="flex align-center">
					<checkbox-group style="margin-right: 10upx;">
						<checkbox @tap="changeChecked(index)" style="transform: scale(0.7);" class="round sx-check" :class="item.checked==true?'checked':''" :checked="item.checked" ></checkbox>
					</checkbox-group>
					<image :src="item.img" mode=""></image>
				</view>
				<view class="cart-ycontent" style="width: 420upx;">
					<view class="cart-des">{{item.goods_name}}</view>
					<view>
						<view class="text-gray">{{item.type}}</view>
						<view class="flex justify-between">
							<view class="text-red text-bold text-lg" style="line-height: 2.6em;">{{'¥' + item.price + '.00'}}</view>
							<uni-number-box @change="changeMath" v-model="item.num" style="width:80px; margin-right: 40upx;" :min="1" :max="100"></uni-number-box>
						</view>
						
					</view>
					
				</view> 
			</view>
			</view>
		</scroll-view>
		
		<!-- 底部合计金额 -->
		<view class="cart-total flex justify-between align-center">
			<checkbox-group @change="changeAll">
				<checkbox style="transform: scale(0.7);" :class="checked==true?'checked':''" :checked="checked" class="round" ></checkbox>
				<text style="font-size: 110%; margin-left: 10upx;">全选</text>
			</checkbox-group>
			<view class="" style="position: fixed; left: 180upx;">合计<text class="text-orange">¥:{{sum}}</text></view>
			<view>
				<view class="cu-btn bg-gradual-red round">去结算</view>
			</view>
		</view>
		<!-- 内容部分 -->
		
	</view>
</template>

<script>
	import uniNumberBox from "@/components/uni-number-box/uni-number-box.vue"
	export default {
		data() {
			return {
				isTool: false,  
				// 商品列表，真实开发环境下，调接口来填充
				lists: [],
				selectId: [], //选中的商品
				totalMoney: 0,  //总价
				checkNum: 0,  //选择的商品数量(结算需要显示的数量)
				checkAllFlag:false,  //是否全选
				checked: true,
				scrollTop: 0,
				isShowTop: false,
				old: {
				    scrollTop: 0
				}
			}
		},
		
		onLoad(e) {
			console.log(this.lists);
			this.getList();
		},
		computed:{
			sum(){
				var he = 0;
				this.lists.forEach(item => {
					if(item.checked == true){
						he += item.num * item.price;
					}
				});
				return he.toFixed(2);
			}
		},
		components: {
			uniNumberBox
			}, 
		methods: {
			//单选改变选中状态
			changeChecked(index){
				this.lists[index].checked = this.lists[index].checked?false:true;
				var selectd = this.lists.filter(item => {return !item.checked});
				selectd.length==0?this.checked=true:this.checked=false;
			},
			changeMath(val){
				if(val == 0){
					
				}
			},
			//全选
			changeAll(e){
				this.lists.forEach(item => {
					item.checked = !this.checked;
				})
				this.checked?this.checked=false:this.checked=true;
			},
			// 删除选中的商品
			deleteGoods() {
				var its = this;
				uni.showModal({
					confirmText:"确定",
					content: "您确定要把商品移除购物车吗",
					title: "删除提示",
					success(res) {
						if(res.confirm){
							its.lists = its.lists.filter(item => {
								return !item.checked;
							});
						}
						
						// console.log(res)
					}
				})
			},
			//监控滚动
			Scroll(e){
			
			    this.old.scrollTop = e.detail.scrollTop
			    this.old.scrollTop = e.detail.scrollTop
			    if (this.old.scrollTop > 100){
			        this.isShowTop = true
			    }else {
			        this.isShowTop = false
			    }
			
			},
			// 单选
			onSel(index, flag) {
				let that = this;
				that.$store.commit('selectItem', { index, flag });
			},
			//获取数据
			getList(){
				var data =  [
					{
						id: '1',
						shop_name: '同玺服饰专营店',
						goods_name: '短袖T恤男2020夏季新款半袖体恤衫休闲时尚刺绣男装舒适透气大码衣服 T126白',
						price: 58,
						img: '../../static/goods/1.png',
						num: 1,
						checked: true,
						type: "白色 黑色"
					},{
						id: '2',
						shop_name: '炫酷度服饰专营店',
						goods_name: '绫帛【4件装】长袖T恤男 2020春季新品印花圆领长袖上衣男装韩版修身男士秋装',
						price: 66,
						img: "../../static/goods/2.png",
						num: 1,
						checked: true,
						type: "蓝色 黑色"
						
					},{
						id: '3',
						shop_name: '墨写服装专营店',
						goods_name: '尊尚鸟 短袖T恤男夏季韩版潮流短袖男士半袖t恤印花休闲修身青年学生体恤衣服',
						price: 75,
						img: '../../static/goods/4.png',
						num: 2,
						checked: true,
						type: "绿色 白色"
						
						
					},{
						id: '4',
						shop_name: '千泽服装专营店',
						goods_name: '简柯林短袖t恤男装半袖男士衣服夏季时尚潮流印花打底衫潮牌T恤 430黄色 XL ',
						price: 46,
						img: '../../static/goods/1.png',
						num: 1,
						checked: true,
						type: "白色 黑色"
						
					},{
						id: '5',
						shop_name: '足冠运动户外专营店',
						goods_name: '花花公子短袖套装男T恤裤子2020夏季新品衣服饰修身潮圆领宽松t恤衫休闲裤套',
						price: 99,
						img: '../../static/goods/2.png',
						num: 1,
						checked: true,
						type: "白色 黑色"
						
					},{
						id: '6',
						shop_name: '全息服饰专营店',
						goods_name: '欧洲站潮牌烫钻短袖T恤男修身半袖潮流打底衫体恤2020新款夏季男装衣服 黑色',
						price: 78,
						img: '../../static/goods/3.png',
						num: 1,
						checked: true,
						type: "白色 黑色"
					},{
						id: '6',
						shop_name: '全息服饰专营店',
						goods_name: '欧洲站潮牌烫钻短袖T恤男修身半袖潮流打底衫体恤2020新款夏季男装衣服 黑色',
						price: 78,
						img: '../../static/goods/3.png',
						num: 1,
						checked: true,
						type: "白色 黑色"
					},{
						id: '6',
						shop_name: '全息服饰专营店',
						goods_name: '欧洲站潮牌烫钻短袖T恤男修身半袖潮流打底衫体恤2020新款夏季男装衣服 黑色',
						price: 78,
						img: '../../static/goods/3.png',
						num: 1,
						checked: true,
						type: "白色 黑色"
					},{
						id: '6',
						shop_name: '全息服饰专营店',
						goods_name: '欧洲站潮牌烫钻短袖T恤男修身半袖潮流打底衫体恤2020新款夏季男装衣服 黑色',
						price: 78,
						img: '../../static/goods/3.png',
						num: 1,
						checked: true,
						type: "白色 黑色"
					},{
						id: '6',
						shop_name: '全息服饰专营店',
						goods_name: '欧洲站潮牌烫钻短袖T恤男修身半袖潮流打底衫体恤2020新款夏季男装衣服 黑色',
						price: 78,
						img: '../../static/goods/3.png',
						num: 1,
						checked: true,
						type: "白色 黑色"
					},{
						id: '6',
						shop_name: '全息服饰专营店',
						goods_name: '欧洲站潮牌烫钻短袖T恤男修身半袖潮流打底衫体恤2020新款夏季男装衣服 黑色',
						price: 78,
						img: '../../static/goods/3.png',
						num: 1,
						checked: true,
						type: "白色 黑色"
					}];
					this.lists = data	
			},
		}
	}
</script>

<style>
	.cart-top {
		position: fixed;
		top: 90upx;
		background-color: #f7f5f6;
		display: flex;
		justify-content: space-between;
		height: 80upx;
		align-items: center; 
		width: 750upx;
		padding-left: 30upx;
		padding-right: 30upx;
	}
	.count-box{
		font-size: 26upx;
		color: #999;
	}
	.all-num {
		color: #a8700d;
	}
	.set-btn{
		color: #a8700d;
	}
		
	.cart-scroll{
		margin-top: 80upx;
		margin-bottom: 100upx;
		height: calc(100vh - 180px);
	}
	.cart-item{
		display: flex;
		justify-content: space-between;
		padding: 20upx 20upx 20upx 20upx;
		margin-top: 20upx;
	}
	.cart-item image{
		width: 200upx;
		height: 200upx;
	}
	.cart-des{
		font-size: 110%;
		font-weight: bold;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}
	.cart-ycontent{
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		/* padding-top: 40upx; */
	}
	.cart-total{
		font-size: 26upx;
		color: #999;
		position: fixed;
		bottom: 90upx;
		width: 750upx;
		height: 100upx;
		background-color:#f7f5f6;
		padding-left: 30upx;
		padding-right: 30upx;
	}
</style>
