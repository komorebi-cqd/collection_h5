<template>
  <view class="quantum" :class="{sincere: gold}">
        <text class="quantum-text">限量</text>
        <text class="quantum-number" :class="{gold: gold}">{{quantity}}份</text>
    </view>
</template>

<script>
export default {
    props:{
        quantity: Number,
        gold: {
            type: Boolean,
            default: false,
        }
    },
    data(){
        return{

        }
    }
}
</script>

<style lang="scss" scoped>
.quantum{
    background-color: #D8D8D8;
    border-radius: 8rpx;
    color: #333;
    font-size: 24rpx;
    display: inline-block;
    margin: 18rpx 0;
    padding: 2rpx 0;
    .quantum-text{
        background-color: #FFDEA0;
        border-radius: 4px;
        padding: 2rpx 10rpx;
    }
    
    .quantum-number{
        padding: 0 16rpx 0 10rpx;
        color: #333;
        &.gold{
            color: #FFDEA0;
        }
    }
    &.sincere{
        background-color: rgba(216,216,216,.5);
    }
}
</style>