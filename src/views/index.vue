<template>
  <div style="text-align:center">
    <h2>Demo</h2>

    <div style="position: relative">
      <sms :ms="60" @fn="smsSend">
        <span class="content-sms" slot="content">短信验证码</span>
      </sms>
    </div>

    <div>
      <slider value=35></slider>
    </div>
  </div>
</template>
<script>
import sms from "../components/smsCountDown";
import slider from '../components/slider'
export default {
  name: "index",
  components: {
    sms,
    slider
  },
  methods: {
    smsSend() {
      console.log("send sms code");
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
.input{
    padding: 15px;

}
</style>
