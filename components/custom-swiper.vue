<template>
    <view class="banner-wrap">
        <swiper
            class="banner-swiper"
            :current="current"
            indicator-active-color="#BE3620"
            indicator-color="rgba(255,226,212,0.5)"
            :autoplay="autoplay"
            :duration="duration"
            :interval="interval"
            :circular="circular"
            previous-margin="0"
            next-margin="0"
            @change="swiperChange"
        >
            <swiper-item
                v-for="(item, index) in bannerList"
                :key="index"
                @click="handleJump(item.link)"
            >
                <view class="banner-swiper-item">
                    <image
                        :src="item.image"
                        mode="aspectFill"
                        class="banner-swiper-img"
                        :class="current == index ? '' : 'active'"
                    ></image>
                </view>
            </swiper-item>
        </swiper>
        <view class="indicator-list">
            <view class="indicator" :class="{active: current === index}" v-for="(item,index) in bannerList" :key="index"></view>
        </view>
    </view>
</template>

<script>
export default {
    name: "index-swiper",
    props: {
        bannerList: {
            type: Array,
            default: () => {
                return [];
            },
        },
    },
    data() {
        return {
            current: 0, //当前图片
            indicatorDots: true, //是否显示面板指示点
            autoplay: true, //是否自动切换
            interval: 3000, //自动切换时间间隔
            duration: 500, //滑动动画时长
            circular: true, //是否采用衔接滑动，即播放到末尾后重新回到开头
            // previousMargin:"17px",//前边距
            // nextMargin:"17px",//后边距
        };
    },
    methods: {
        swiperChange(e) {
            let { current, source } = e.detail;
            //只有页面自动切换，手动切换时才轮播，其他不允许
            if (source === "autoplay" || source === "touch") {
                this.current = current;
            }
        },
        handleJump(link) {
            if (link.startsWith("http")) {
                window.open(link);
            } else {
                uni.navigateTo({
                    url: link,
                });
            }
        },
    },
};
</script>

<style lang="scss" scoped>
.banner-wrap {
    width: 100%;
    margin: 30rpx auto 0;
    .banner-swiper {
        height: 360rpx;
        .banner-swiper-item {
            border-radius: 40rpx;
            width: 100%;
            height: 360rpx;
            overflow: hidden;
            padding: 0 30rpx;
            box-sizing: border-box;
        }

        .banner-swiper-img {
            display: block;
            margin: auto;
            width: 100%;
            height: 100%;
            border-radius: 40rpx;
        }
        .active {
            transition: all 0.2s linear 0s;
            transform: translateY(0);
        }
    }
    .indicator-list{
        display: flex;
        align-items: center;
        justify-content: center;
        margin-top: 14rpx;
        .indicator{
            width: 8rpx;
            height: 8rpx;
            background: #999;
            border-radius: 50%;
            transition: all 0.2s;
            margin: 0 4rpx;
            &.active{
                background-color: #ffffff;
                width: 20rpx;
                height: 8rpx;
                border-radius: 4rpx;
            }
        }
    }
}
</style>
