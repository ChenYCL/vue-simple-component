<template>
    <div class="nav-bar" :style="`background:${color}`">
        <div style="text-align: left">
            <i v-if="leftShow&&leftIcon" @click="goBack" class="icon"
               :style="`background-image:url('${leftIcon}')`"></i>
            <i v-if="leftShow&&!leftIcon" @click="goBack" class="icon icon-default"></i>
        </div>
        <div style="text-align: center" class="_title">{{title}}</div>
        <div style="text-align: right">
            <i @click="rEv" class="icon2" v-if="rightIcon_left"
               :style="`background-image:url('${rightIcon_left}')`"></i>
            <i @click="rEv" class="icon1" v-if="rightIcon&&!$slots.hasOwnProperty('rightContent')"
               :style="`background-image:url('${rightIcon}')`"></i>
            <span class="rText" :style="`color:${rColor}`" @click="rEv"
                  v-if="rText&&!$slots.hasOwnProperty('rightContent')">{{rText}}</span>
            <slot name="rightContent"></slot>
        </div>
    </div>
</template>
<script>
  /**
   * 引用方式
   *   <t-nav r-text="记录" left-icon="bg.png" :left-show="true" :right-icon="require('../../assets/images/home_c2c_press.svg')" :back-func="func1" :right-ev="func2" title="首页1"></t-nav>
   */

  export default {
    name: "index",
    props: {
      color: { // 背景色
        type: String,
        default: ''
      },
      leftIcon: { //  左侧图标地址
        type: String,
        default: ''
      },
      leftShow: {  // 是否显示返回按钮
        type: Boolean,
        default: true
      },
      title: { // 居中标题
        type: String,
        default: '首页'
      },
      rightIcon: { // 右侧图标地址1  外侧右边
        type: String,
        default: ''
      },
      rightIcon_left: { // 右侧图标地址2  内侧右边
        type: String,
        default: ''
      },
      backFunc: { // 左侧event 默认返回路由上级
        type: Function,
        default: null
      },
      rText: {
        type: String,
        default: ''
      },
      rColor: {
        type: String,
        default: ''
      },
      rightEv: { // 右侧event
        type: Function,
        default: () => {
          return null
        }
      }

    },
    methods: {
      goBack () {
        if (this.backFunc) {
          this.backFunc()
          return
        }
        console.log("-------goBack-------");
        if (typeof plus == "object") {
          // eslint-disable-next-line
          let webview = plus.webview.getLaunchWebview();
          webview.back();
        } else {

          this.$router.go(-1)
        }
      },
      rEv () {
        if (this.rightEv) {
          this.rightEv()
          return
        }
      }
    }
  }
</script>
<style scoped lang="scss">
    .rightIcon2 {
        border: 1px solid red;
    }

    .nav-bar {
        box-sizing: content-box;
        height: 24px;
        padding: 10px 14px !important;
        font-size: 18px;
        background: #272E73;
        font-weight: 500;
        color: white;
        display: grid;
        grid-template-columns: 1fr 2fr 1fr;

        &.div {
            line-height: 24px;
            position: relative;
        }

        .icon {
            background-position: center center;
            background-repeat: no-repeat;
            background-size: 100% 100%;
            border-radius: 50%;
            border: 0;
            display: inline-block;
            height: 24px;
            width: 24px;
        }

        .icon-default {
            background-image: url("../../assets/top_return.png");
        }

        ._title {
            font-size: 18px;
            font-weight: 500;
            color: rgba(255, 255, 255, 1);
            line-height: 24px !important;
        }

        .rText {
            color: white;
            font-size: 14px;
            font-weight: 400;
        }

        .icon1 {
            background-position: center center;
            background-repeat: no-repeat;
            background-size: 100% 100%;
            display: inline-block;
            height: 24px;
            width: 24px;
        }

        .icon2 {
            background-position: center center;
            background-repeat: no-repeat;
            background-size: 100% 100%;
            display: inline-block;
            height: 24px;
            width: 24px;
            margin-right: 10px;
        }
    }
</style>