<template>
    <view class="person">
		<!-- 第一部分开始 -->
		<view class="flex justify-between bg-white person-content1">
			<view class="flex">
				<view><image class="user-logo" src="../../static/goods/1.png" mode=""></image></view>
				<view style="margin-left: 20upx;">
					<view class="user-name">
						<text>沧海忘了情</text>
						<view class="cu-btn bg-yellow sm radius">铂金会员</view>
						</view>
					<view style="margin-top: 25upx;">
						<view class="cu-tag round line-blue sm">182****7918</view>
						<view class="cu-tag round line-blue sm">会员认证</view>
					</view>
				</view>
			</view>
			<view class="flex align-center">
				<!-- <button class="cu-btn line-red round"> -->
					<view class="cuIcon-settings text-black lg pe-settings"></view>
					
				<!-- </button> -->
			</view>
		</view>
		<!-- 第一部分结束 -->
		
		<!-- 省钱月卡 -->
			<view class="yueka-fa">
				<view class="yueka">
					<view class="flex align-center">
						<text style="font-size: 110%;">省钱月卡</text>
						<text style="margin-left: 10upx; margin-right: 10upx;">|</text>
						<text>帮你省201块</text>
					</view>
					<view class="flex align-center">
						<button class="cu-btn sm round bg-red">领取201元优惠券</button>
						<view class="cuIcon-right"></view>
					</view>
				</view>
			</view>
		<!-- 省钱月卡 -->
		
		<!-- 订单部分 -->
		<view class="flex justify-center flex-direction bg-white" style="margin-top: 2upx;">
			<view style="width: 90%;" class="flex justify-between">
				<text style="font-size: 120%;">我的订单</text>
				<text class="text-gray">查看全部</text>
			</view>
			<view class=" flex justify-around align-center" style="width: 700upx; height: 120upx; border-radius: 20upx;">
				<view v-for="(item,index) in orders" :key="index" class="flex align-center flex-direction" style="position: relative;">
					<view :class="item.icon" style="font-size: 60upx;color: gray;"></view>
					<view v-if="item.num!=0" style="position: absolute; top: 0upx; right: 0upx;" class="cu-tag bg-red round sm">
						{{item.num}}
					</view>
					<view>{{item.text}}</view>
				</view>
			</view>
		</view>
		<!-- 订单部分 -->
    </view>
</template>

<script>

    export default {
        name: "person",
        data(){
            return {
				orders: [
					{
						text: "待付款",
						icon: "cuIcon-pay",
						num: 2,
						id: 1
					},{
						text: "待分享",
						icon: "cuIcon-share",
						num: 0,
						id: 2
					},{
						text: "待发货",
						icon: "cuIcon-time",
						num: 0,
						id: 3
					},{
						text: "待收货",
						icon: "cuIcon-deliver",
						num: 5,
						id: 4
					},{
						text: "待评价",
						icon: "cuIcon-comment",
						num: 0,
						id: 5
					}
				]
            }
        },
        methods: {
        }
    }
</script>

<style scoped lang="less">
.person-content1{
	padding: 30upx 30upx 30upx 30upx;
	background-color: #F8F8F8;
}
.user-logo{
	width: 120upx;
	height: 120upx;
}
.user-name{
	font-size: 110%;
	display: flex;
	align-items: center;
}

.pe-settings{
	font-size: 50upx; 
	font-weight: 700;
	position: fixed;
	right: 20upx;
	top: 40upx;
}

.yueka-fa{
	background-color: #F8F8F8;
	display: flex;
	justify-content: center;
}
.yueka{
	width: 660upx;
	height: 80upx;
	background-color: #FADBD9;
	border-top-left-radius: 25upx;
	border-top-right-radius: 25upx;
	display: flex;
	justify-content: space-between;
	align-items: center;
	color: #DD514C;
	padding-left: 20upx;
	padding-right: 20upx;
}
</style>