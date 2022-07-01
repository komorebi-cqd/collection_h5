<template>
  <view class="description">
      <CustomNavBar :isGasket="false"></CustomNavBar>
      <view class="collection-bg">
          <view class="collection">
                <view class="collection-border">
                    <image class="details-img" src="../../static/test.png" mode="aspectFill"></image>
                </view>
          </view>
          <view class="rarity" v-if="false">
              <image mode="aspectFill" src="../../static/energy/rarity-icon.png"></image>
          </view>
      </view>
      <view class="collection-content">
        <view class="collection-int">
            <view class="int-title">无敌的我</view>
            <QuantumText :quantity="999"></QuantumText>
            <view class="int-bottom">
                <view>西安博物院</view>
                <!-- <view>兑换上限：<text class="int-bottom-number">1</text></view> -->
            </view>
        </view>

        <view class="collection-des">
            <view class="des-title">作品描述</view>
            <view class="des-img">
                <image class="details-img" src="../../static/test.png" mode="widthFix"></image>
            </view>
        </view>
        <BuyTip />
      </view>
      
      <FooterSection class="footer-section" bgColor="#282B2A">
          <text class="footer-energy">￥888.00</text>
          <button class="footer-button" @click="handleBuy">购买</button>
      </FooterSection>
  </view>
</template>

<script>
import CustomNavBar from '../../components/custom-nav-bar.vue'
import FooterSection from '../../components/footer-section.vue'
import QuantumText from '../../components/quantum-text.vue'
import BuyTip from '../../components/buy-tip.vue'


export default {
    props:{
        
    },
    data(){
        return{

        }
    },
    components: {CustomNavBar,FooterSection,QuantumText,BuyTip},
    methods:{
        handleBuy(){
            console.log(111);
        }
    }
}
</script>

<style lang="scss" scoped>
@import "../../common/index.scss";

.description{
    @include full-screen-color;
    padding-bottom: 200rpx;
}

.collection-bg{
    width: 100%;
    height: 760rpx;
    background: url('../../static/energy/collection-bg.png') left 0 top 0 no-repeat;
    background-size: 100% 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    .collection{
        width: 450rpx;
        height: 450rpx;
        position: relative;
        image{
            width: 100%;
            height: 100%;
            border-radius: 30rpx;
        }
        .collection-border{
            --border-radius: 30rpx;
            --border-width: 4rpx;
            appearance: none;
            position: relative;
            padding: 10rpx;
            border: 0;
            font-weight: 500;
            color: #fff;
            z-index: 2;
            width: 100%;
            height: 100%;
            image{
                padding: 4rpx 0 0 4rpx;
            }
            &::after{
                --m-i: linear-gradient(#000, #000);
                --m-o: content-box, padding-box;
                content: "";
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
                height: 100%;
                z-index: -1;
                padding: var(--border-width);
                border-radius: var(--border-radius);
                background-image: conic-gradient(#F59EAA, #7FDEFF, #F59EAA);
                -webkit-mask-image: var(--m-i), var(--m-i);
                mask-image: var(--m-i), var(--m-i);
                -webkit-mask-origin: var(--m-o);
                mask-origin: var(--m-o);
                mask-clip: var(--m-o);
                mask-composite: exclude;
                -webkit-mask-composite: destination-out;
            }
        }
    }
    .rarity{
        width: 116rpx;
        height: 116rpx;
        position: absolute;
        right: 36rpx;
        bottom: 0;
        image{
            width: 100%;
            height: 100%;
        }
    }
}
.collection-content{
    padding: 30rpx 30rpx 0;
    font-size: 36rpx;
}

.collection-int{
    width: 100%;
    height: 220rpx;
    background-color: #FFFFFF;
    border-radius: 30rpx;
    padding: 30rpx;
    box-sizing: border-box;
    .int-title{
        font-weight: bold;
        text-overflow: -o-ellipsis-lastline;
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 1;
        line-clamp: 1;
        -webkit-box-orient: vertical;
        word-break: break-all;
    }
    .int-bottom{
        display: flex;
        justify-content: space-between;
        color: #999999;
        font-size: 24rpx;
        .int-bottom-number{
            color: #333333;
            font-weight: bold;
        }
    }
}

.collection-des{
    margin: 30rpx 0 56rpx;
    min-height: 500rpx;
    background-color: #fff;
    border-radius: 30rpx;
    .des-title{
        padding: 30rpx 0 0 24rpx;
        font-weight: bold;
        position: relative;
        display: inline-block;
        z-index: 9;
        margin-bottom: 40rpx;
        &::after{
            @include ball-bg;
        }
    }
}
.des-img{
    
    image{
        width: 100%;
        margin-bottom: -28rpx;
        border-radius: 0 0 28rpx 28rpx;
    }
}
.foot-fixed{
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 36rpx;
}
.footer-energy{
    color: #FFF;
}
.footer-button{
    min-width: 240rpx;
    height: 80rpx;
    background: linear-gradient(90deg, #F79DA8 0%, #94E2FC 100%);
    border-radius: 45rpx;
    color: #000;
    padding: 0 26rpx;
    box-sizing: border-box;
    font-size: 32rpx;
    margin: 0;
    @include flexCenter;
    &[disabled]{
        opacity: 0.5;
        color: inherit;
    }
}

</style>