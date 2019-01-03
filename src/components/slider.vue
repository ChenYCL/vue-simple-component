<template>
  <section id="slider">
    <div class="bar" ref="bar">
      <span
        class="drag-dot"
        ref="drag_dot"
        @drag="dragEvent($event)"
        :value="value"
        :style="`transform: translateX(${value}%)`"
      ></span>
      <span
        class="dot"
        v-for="i in interval"
        :key="i"
        @click="interClick((i-1)*25)"
        :style="`left:${(i-1)*25}%;`"
      ></span>
    </div>
  </section>
</template>

<script>
export default {
  name: "slider",
  data() {
    return {
      DOMRect: null,
      isMobile: false
    };
  },
  computed: {},
  props: {
    interval: {
      type: Number,
      default: 5
    },
    sliderStyle: {
      type: Object,
      default: () => {
        return {};
      }
    },
    value: {
      type: String | Number,
      default: () => {
        return 0;
      }
    }
    // dragEvent:{
    //   type:Function,
    //   default:null
    // },
    // tapEvent:{
    //   type:Function,
    //   default:null
    // }
  },
  methods: {
    dragEvent($event) {
      console.log($event.clientX);
      let PosiX = $event.clientX;
      this.value = PosiX - this.DOMRect.x;
    //   console.log(PosiX - this.DOMRect.x);

    },
    deviceJudge() {
      var sUserAgent = navigator.userAgent.toLowerCase();
      var bIsIpad = sUserAgent.match(/ipad/i) == "ipad";
      var bIsIphoneOs = sUserAgent.match(/iphone os/i) == "iphone os";
      var bIsMidp = sUserAgent.match(/midp/i) == "midp";
      var bIsUc7 = sUserAgent.match(/rv:1.2.3.4/i) == "rv:1.2.3.4";
      var bIsUc = sUserAgent.match(/ucweb/i) == "ucweb";
      var bIsAndroid = sUserAgent.match(/android/i) == "android";
      var bIsCE = sUserAgent.match(/windows ce/i) == "windows ce";
      var bIsWM = sUserAgent.match(/windows mobile/i) == "windows mobile";
      if (
        bIsIpad ||
        bIsIphoneOs ||
        bIsMidp ||
        bIsUc7 ||
        bIsUc ||
        bIsAndroid ||
        bIsCE ||
        bIsWM
      ) {
        // document.writeln("phone");
        this.isMobile = true;
      } else {
        // document.writeln("pc");
      }
    },
    mobileEventBind() {
      this.$refs.drag_dot.addEventListener("touchmove", event => {
        // this.value =
        console.log(event.touches[0]);
        let PosiX = event.touches[0].clientX;
        console.log(PosiX - this.DOMRect.x);
        this.value = PosiX - this.DOMRect.x;
      });
    },
    interClick(_value) {
      console.log(_value);
    }
  },
  created() {
    this.$nextTick(() => {
      this.DOMRect = this.$refs.bar.getBoundingClientRect();
      console.log(this.DOMRect);
      this.deviceJudge();
      if (this.isMobile) {
        this.mobileEventBind();
      }
    });
  }
};
</script>

<style scoped lang="scss">
#slider {
  padding: 15%;
  .bar {
    position: relative;
    display: inline-block;
    height: 10px;
    width: 100%;
    background: grey;
    border-radius: 10px;
    .drag-dot {
      display: inline-block;
      position: absolute;
      z-index: 3;
      height: 20px;
      width: 20px;
      background: red;
      border-radius: 50%;
      transform: translate3d(-25%, -25%, 0px);
      left: 0;
      cursor: pointer;
    }
    .dot {
      display: inline-block;
      position: absolute;
      height: 15px;
      width: 15px;
      background: grey;
      border-radius: 50%;
      transform: translate3d(-25%, -25%, 0px);
      z-index: 2;
      left: 0;
    }
  }
}
</style>