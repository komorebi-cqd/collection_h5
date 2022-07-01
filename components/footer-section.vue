<template>
    <view class="foot-fixed" :style="{backgroundColor: bgColor}">
        <slot></slot>
    </view>
</template>

<script>
export default {
    data() {
        return {
        };
    },
    props: {
        bgColor:{
            type: String,
            default: '#FFFFFF'
        }
    }
}
</script>

<style lang="scss" scoped>
.foot-fixed {
    position: fixed;
    width: 100%;
    height: 140rpx;
    padding: 0 33rpx;
    box-sizing: border-box;
    bottom: 0;
    left: 0;
    z-index: 2;
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    align-items: center;
}
</style>
