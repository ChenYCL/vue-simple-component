<template>
    <div style="text-align:center">
        <t-nav title="我是导航条" color="green" r-text="右侧文字"></t-nav>
        <p style="color: red">1.sheet</p>
        <button style="background: yellow;border: 1px solid yellowgreen" @click="$refs.sheet.show=true">点击sheet</button>
        <sheet ref="sheet"></sheet>


        <p style="color: red">2.bar</p>
        <bar :h="20" color="green"></bar>

        <p style="color: red">3.modal弹窗</p>

        <button @click="$refs.$modal.modal=true">modal点击</button>
        <modal ref="$modal" title="我是标题">
            <div slot="content">
                <h1>内容体标题</h1>
                <p>正文</p>
            </div>
        </modal>

        <p style="color: red">4.message提示</p>
        <button @click="msg">点我弹信息</button>

        <p style="color: red">5.短信验证码倒计时</p>
        <div>
            <sms :ms="60" @fn="smsSend">
                <span class="content-sms" slot="content">短信验证码</span>
            </sms>
        </div>

        <div>
            <p>slider滑块，只支持移动端</p>
            <slider value="35"></slider>
        </div>
        <p>高度height 10,宽度 width 400,颜色 color:green</p>
        <div style="display:flex;justify-content: center;">
            <mprogress height="10" width="400" color="red" innercolor="yellow"/>
        </div>
    </div>
</template>
<script>
  import Vue from 'vue'
  import sms from "../components/smsCountDown";
  import slider from "../components/slider";
  import mprogress from "../components/mprogress";
  import tNav from '../components/nav/index.vue'
  import sheet from '../components/ch_bottom-sheet/index'
  import bar from '../components/lineBar/index'
  import modal from '../components/modal/index.vue'
  import radio from '../components/radio/radio'

  // message注册
  import Message from "../components/message/index.js";

  Vue.prototype.$message = Message;

  export default {
    name: "index",
    components: {
      sms,
      slider,
      mprogress,
      tNav,
      sheet,
      bar,
      modal,
      radio
    },
    methods: {
      smsSend () {
        console.log("send sms code");
      },
      msg () {
        this.$message({
          msg: '收到消息',
          duration: 3000, //可选参数
        });
      }
    }
  };
</script>
<style scoped lang="scss">
    .content-sms {
        display: inline-block;
        position: absolute;
        /*width: 10%;*/
        top: 33px;
        right: 15px;
        border-left: 1px solid #cccccc;
        padding-left: 20px;
        padding-right: 10px;
        color: green;
        cursor: pointer;
    }

    .input {
        padding: 15px;
    }
</style>
