<template>
    <view class="nav-bar-container">
        <view class="nav-bar-wrap" :class="{'nav-bar-wrap-fixed': isFixed}">
            <!-- 安卓或者微信要加的 -->
            <view :style="{ height: statusBarHeight + 'rpx' }"></view>
            <view class="nav-bar" :style="{backgroundColor: bgColor}">
                <view class="nav-bar-left">
                    <image v-if="isShowLeft" @click="goBack" class="back" src="../static/energy/back.png"></image>
                    <slot name="left"></slot>
                </view>
                <view class="nav-bar-center">
                    <slot></slot>
                </view>
                <view class="nav-bar-right">
                    <slot name="right"></slot>
                </view>
            </view>
        </view>
        <!-- 垫片 -->
        <view :style="{ height: 88 + statusBarHeight + 'rpx' }" v-if="isGasket"></view>
    </view>
</template>

<script>
export default {
    name: "CustomNavBar",
    data() {
        return {
            statusBarHeight: 0,
        };
    },
    props:{
        isShowLeft: {
            type: Boolean,
            default: true
        },
        //如果是false则会和导航重合
        isGasket: {
            type: Boolean,
            default: true
        },
        bgColor: {
            type: String,
            default: 'transparent'
        },
        isFixed: {
            type: Boolean,
            default: true
        },
    },
    created() {
        this.getSystemInfo();
    },
    methods: {
        getSystemInfo() {
            const systemInfo = uni.getSystemInfoSync();
            systemInfo.statusBarHeight &&
                (this.statusBarHeight = systemInfo.statusBarHeight + 20);
        },
        goBack(){
            const pages =getCurrentPages();
            console.log(pages);
            if(pages.length <= 1){
                uni.redirectTo({
                    url: '/pages/index/index',
                });
                return;
            }
            uni.navigateBack({
                delta: 1
            });
        }
    },
};
</script>

<style lang="scss" scoped>
@import '../common/index.scss';
.nav-bar-container{
    width: 100%;
}
.nav-bar-wrap {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 9;
}
.nav-bar-wrap-fixed{
    position: fixed;
    top: 0;
    left: 0;
}
.nav-bar {
    height: 88rpx;
    line-height: 88rpx;
	box-sizing: border-box;
	display: flex;
    align-items: center;
    .back{
        width: 40rpx;
        height: 40rpx;
		// padding-left: 42rpx;
    }
    .nav-bar-left{
        @include flexCenter;
		flex: 1 1 220rpx;
    }
    .nav-bar-center{
        font-size: 36rpx;
        font-weight: normal;
        text-align: center;
        color: #fff;
		flex: 1 1 auto;
    }
	.nav-bar-right{
		flex: 1 1 220rpx;
	}
}
</style>