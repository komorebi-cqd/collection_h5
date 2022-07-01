<template>
  <view class="buy-tip">
      <view class="buy-tip-title">购买须知</view>
      <view class="buy-tip-item">
          <view class="tip-number">1</view>
          <text>数字藏品为虚拟数字商品，而非实物，仅限实名认证为年满14周岁的中国大陆用户购买。</text>
      </view>
      <view class="buy-tip-item">
          <view class="tip-number">2</view>
          <text>数字藏品的版权由发行方或原创者拥有，除另行取得版权拥有者书面同意外，用户不得将数字藏品用于任何商业用途。本商品一经售出，不支持退换。</text>
      </view>
      <view class="buy-tip-item">
          <view class="tip-number">3</view>
          <text>本商品源文件不支持本地下载，请勿对数字藏品进行炒作、场外交易、欺诈，或以任何其他非法方式进行使用。</text>
      </view>
  </view>
</template>

<script>
export default {
    data(){
        return{

        }
    }
}
</script>

<style lang="scss" scoped>
@import '../common/index.scss';

.buy-tip{
    width: 100%;
    padding: 28rpx 24rpx;
    background-color: #FFFFFF;
    border-radius: 30rpx;
    .buy-tip-title{
        position: relative;
        z-index: 9;
        display: inline-block;
        margin-bottom: 36rpx;
        &::after{
            @include ball-bg;
        }
    }
}
.buy-tip-item{
    display: flex;
    justify-content: space-between;
    .tip-number{
        width: 28rpx;
        height: 28rpx;
        line-height: 28rpx;
        border-radius: 50%;
        background-color: #000000;
        font-size: 24rpx;
        color: #FFFFFF;
        flex: 0 0 auto;
        margin-right: 16rpx;
        text-align: center;
    }
    text{
        flex: 1 1 auto;
        font-size: 28rpx;
        line-height: 40rpx;
    }
}
</style>