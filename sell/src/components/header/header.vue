<template>
  <div class="header">
    <div class="conter-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="conter">
        <div class="title">
          <span class="brand">品牌</span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达

        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count" @click="showDetail">
        <span class="count">{{seller.supports.length}}个</span>
        <i></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title">公告</span>
      <span class="bulletin-text">{{seller.bulletin}}</span>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <div v-show="detailShow" class="detail" transition="fade">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
          <h1 class="name">{{seller.name}}</h1>
          <div class="star-wrapper">
            <star :size="48" :score="seller.score"></star>
          </div>
          <div class="title">
            <div class="line"></div>
            <div class="text">优惠信息</div>
            <div class="line"></div>
          </div>
          <ul v-if="seller.supports" class="supports">
            <li class="supports-item" v-for="item in seller.supports">
              <span class="icon" :class="classMap[seller.supports[$index].type]"></span>
              <span class="text">{{seller.supports[$index].description}}</span>
            </li>
          </ul>

          <div class="title">
            <div class="line"></div>
            <div class="text">商家公告</div>
            <div class="line"></div>
          </div>
          <div class="bulletin">
            <p class="content">
              {{seller.bulletin}}
            </p>
          </div>
        </div>
      </div>
      <div class="detail-close" @click="hideDetail">
        <span>X</span>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">

  import star from 'components/star/star';

  export default{
    props: {
      seller: {
        type: Object
      }
    },
    data(){
      return {
        detailShow: false
      }
    },
    methods: {
      showDetail() {
        this.detailShow = true;
      },
      hideDetail() {
        this.detailShow = false;
      }
    },
    created(){
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    },
    components: {
      star
    }
  };
</script>

<style lang="less" rel="stylesheet/less">
  .header {
    position: relative;
    overflow: hidden;
    color: #fff;
    background: rgba(7, 7, 7, 0.5);
    .conter-wrapper {
      position: relative;
      padding: 24px 12px 18px 24px;
      font-size: 0;
      .avatar {
        display: inline-block;
        font-size: 14px;
        img {
          border-radius: 2px;
        }
      }
      .conter {
        display: inline-block;
        margin-left: 16px;
        font-size: 14px;
        .title {
          margin: 2px 0 8px 0;
          .brand {
            display: inline-block;
            vertical-align: top;
            background: red;
            width: 30px;
            height: 18px;
            line-height: 18px;
            text-align: center;
          }
          .name {
            font-size: 16px;
            margin-left: 6px;
            line-height: 18px;
            font-weight: bold;
          }
        }
        .description {
          margin-bottom: 10px;
          line-height: 12px;
          font-size: 12px;
        }
        .support {
          font-size: 0;
          .icon {
            display: inline-block;
            vertical-align: top;
            width: 12px;
            height: 12px;
            margin-right: 4px;
            background-size: 12px 12px;
            background-repeat: no-repeat;
            &.decrease {
              background-image: url("decrease.png");
            }
            &.discount {
              background-image: url("discount.png");
            }
            &.special {
              background-image: url("special.png");
            }
            &.invoice {
              background-image: url("invoice.png");
            }
            &.guarantee {
              background-image: url("guarantee.png");
            }
          }
          .text {
            font-size: 10px;
            line-height: 12px;
          }
        }
      }
      .support-count {
        position: absolute;
        right: 12px;
        bottom: 18px;
        padding: 0 8px;
        height: 24px;
        line-height: 24px;
        border-radius: 14px;
        background-color: rgba(0, 0, 0, 0.2);
        color: #fff;
        text-align: center;
        .count {
          font-size: 12px;
        }
      }
    }
    .bulletin-wrapper {
      height: 28px;
      line-height: 28px;
      padding: 0 22px 0 12px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      background: rgba(7, 17, 27, 0.2);
      .bulletin-title {
        display: inline-block;
        width: 22px;
        height: 12px;
        font-size: 10px;
        background-color: red;
        text-align: center;
        line-height: 12px;
        padding: 1px 3px;
        border-radius: 3px;
      }
    }
    .background {
      position: absolute;
      width: 100%;
      height: 100%;
      z-index: -1;
      top: 0;
      left: 0;
      filter: blur(10px);
    }
    .detail {
      position: fixed;
      z-index: 100;
      width: 100%;
      height: 100%;
      overflow: auto;
      background: rgba(7, 17, 27, 0.8);
      top: 0;
      left: 0;
      transition: all 0.5s;
      background-filter:blur(10px);
      &.fade-transition{
        opacity: 1;
        background: rgba(7, 17, 27, 0.8);
      }
      &.fade-enter,&.fade-leave{
        opacity: 0;
        background: rgba(7, 17, 27, 0)
      }
      .detail-wrapper {
        min-height: 100%;
        width: 100%;
        .detail-main {
          margin-top: 64px;
          padding-bottom: 64px;
          .name {
            line-height: 16px;
            text-align: center;
            font-size: 16px;
            font-weight: 700;
            text-align: center;
          }
        }
      }
      .title{
        display: flex;
        width: 80%;
        margin: 30px auto 24px auto;
        .line{
          flex: 1;
          position: relative;
          top: -11px;
          border-bottom: 1px solid rgba(255,255,255,0.2);
        }
        .text{
          padding: 0 12px;
          font-size: 14px;
          font-weight: 700;
        }
      }
      .detail-close {
        position: relative;
        width: 32px;
        height: 32px;
        margin: -64px auto 0 auto;
        clear: both;
        font-size: 32px;
        text-align: center;
        span {
          font-size: 32px;
        }
      }
    }
  }
  .supports{
    width: 80%;
    margin:auto;
    .icon{
      display: inline-block;
      width: 12px;
      height: 12px;
      background-size: 100%;
    }
    .decrease {
      background-image: url("decrease.png");
    }
    .discount {
      background-image: url("discount.png");
    }
    .special {
      background-image: url("special.png");
    }
    .invoice {
      background-image: url("invoice.png");
    }
    .guarantee {
      background-image: url("guarantee.png");
    }
  }
  .bulletin{
    width: 80%;
    margin: auto;
    p{
      padding: 24px 12px;
      font-size: 12px;
      line-height: 24px;
      color: #fff;
      font-weight: 200;
    }
  }
</style>
