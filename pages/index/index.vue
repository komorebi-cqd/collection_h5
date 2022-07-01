<template>
	<view class="home">
		<CustomNavBar :isShowLeft="false" bgColor="#1D201F">
			九色鹿数字藏品馆
		</CustomNavBar>
		<CustomSwiper :bannerList="list3"></CustomSwiper>

		<view class="nav" :class="{'nav-two': nav === 1}">
			<view class="nav-item" :class="{active: nav === 0}" @click="switchNav(0)">数字藏品</view>
			<view class="nav-item" :class="{active: nav === 1}"  @click="switchNav(1)">发售日历</view>
		</view>

		<view class="collection-list">
			<view class="collection-item" v-for="item in 7" :key="item" @click="goDetails">
				<view class="collection-main">
					<image class="main-img" src="https://jiuselu.oss-cn-shenzhen.aliyuncs.com/images/6c551e204db9443d938d74b223f9247d.png"></image>
					<view class="collection-state">
						<image src="../../static/stale.png"></image>
						03月15日 14:00 开售
					</view>
				</view>
				<view class="collection-des">
					<view class="collection-title">九色神鹿九色神鹿九色神鹿九色神鹿-三色鹿九色神鹿-三色鹿九色神鹿-三色鹿</view>
					<QuantumText :quantity="1000" :gold="true"/>
					<view class="collection-bottom">
						<text class="collection-bottom-title">中华博物馆</text>
						<text class="collection-bottom-price">￥18.00</text>
					</view>
				</view>
			</view>
		</view>

		<!-- <view class="sale-calendar">发售日历</view> -->

		<CustomTabbar/>
	</view>
</template>

<script>
	import CustomNavBar from '../../components/custom-nav-bar.vue'
	import CustomTabbar from '../../components/custom-tabbar.vue'
	import CustomSwiper from '../../components/custom-swiper.vue'
	import QuantumText from '../../components/quantum-text.vue'
	export default {
		data() {
			return {
				nav: 0,
				title: 'Hello',
				list3: [
					{
						link: '',
						image: 'https://cdn.uviewui.com/uview/swiper/swiper3.png',
					},
					{
						link: '',
						image: 'https://cdn.uviewui.com/uview/swiper/swiper2.png',
					},
					{
						link: '',
						image: 'https://cdn.uviewui.com/uview/swiper/swiper1.png',
					}
                ],
			}
		},
		components:{CustomNavBar,CustomTabbar,CustomSwiper,QuantumText},
		onLoad() {

		},
		methods: {
			switchNav(cur){
				this.nav = cur;
			},
			goDetails(){
				uni.navigateTo({
					url: '/pages/index/description'
				})
			}
		},
		
	}
</script>

<style lang="scss" scoped>
@import '../../common/index.scss';

.nav{
	position: relative;
	font-size: 36rpx;
	color: #FFFFFF;
	display: flex;
	margin: 46rpx 34rpx 40rpx;
	padding-bottom: 18rpx;
	.nav-item{
		width: 144rpx;
		margin-right: 54rpx;
		transition: all 0.1s;
	}
	.active{
		color: #73EBF2;
	}
	&::before{
		content: '';
		width: 48rpx;
		height: 8rpx;
		background: linear-gradient(90deg, #F79DA8 0%, #94E2FC 100%);
		transition: all 0.3s;
		position: absolute;
		bottom: 0;
		left: 44rpx;
		border-radius: 20rpx;
	}
	&.nav-two{
		&::before{
			left: 244rpx;
		}
	}
}
.collection-list{
	width: 100%;
	padding: 0 34rpx 30rpx;
}
.collection-item{
	width: 100%;
	border-radius: 50rpx;
	background-color: #323534;
	margin-bottom: 30rpx;
	.collection-main{
		position: relative;
		.main-img{
			width: 100%;
			height: 690rpx;
			border-radius: 50rpx;
		}
	}
	.collection-des{
		padding: 30rpx 28rpx;
	}
}
.collection-state{
	display: flex;
	align-items: center;
	position: absolute;
	left: 24rpx;
	top: 34rpx;
	height: 60rpx;
	line-height: 60rpx;
	padding: 0 14rpx;
	font-size: 24rpx;
	color: #000;

	background: #FFFFFF;
	box-shadow: 0px 4rpx 8rpx 0px rgba(0, 0, 0, 0.31);
	border-radius: 30rpx;
	opacity: 0.8;
	backdrop-filter: blur(12rpx);

	image{
		width: 24rpx;
		height: 24rpx;
		margin-right: 6rpx;
	}
}

.collection-des{
	.collection-title{
		color: #FFFFFF;
		font-size: 36rpx;
		@include beyond-ellipsis(2);
	}
	.collection-bottom{
		display: flex;
		justify-content: space-between;
		align-items: flex-end;
		.collection-bottom-title{
			color: #999999;
			font-size: 24rpx;
		}
		.collection-bottom-price{
			font-size: 36rpx;
			color: #78F8FF;
		}
	}
}


</style>