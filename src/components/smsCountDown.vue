<template>
  <section id="smsBtn" :ms="ms" @click="start">
    <slot v-if="status" name="content"></slot>
    <span  class="ms-block green" v-if="!status">{{countms}}s</span>
  </section>
</template>

<script>
export default {
  name: "smsBtn",
  data() {
    return {
      timer: null,
      isStarted: false,
      status: true,
      countms: ""
    };
  },
  props: ["ms", "fn"],
  mounted() {
    this.countms = this.ms;
  },
  methods: {
    start() {
      if (this.isStarted) return;
      this.isStarted = true;
      if (this.isStarted && this.countms == this.ms) {
        this.$emit("fn");
      }
      this.status = false;
      this.timer = setInterval(() => {
        this.countms -= 1;
        if (this.countms <= 0) {
          this.isStarted = false;
          this.status = true;
          this.countms = this.ms;
          clearInterval(this.timer);
        }
      }, 1000);
    }
  },
  beforeDestroy() {
    clearInterval(this.timer);
  }
};
</script>

<style scoped lang="scss" >
#smsBtn {
  position: relative;
}
.green {
  color: green !important;
  font-size: 12px;
}
.hide {
  visibility: hidden;
}
.show {
  visibility: visible;
}

.ms-block {
  border-left: 1px solid rgba(0, 0, 0, 0.1);
  padding-left: 20px;
  width: 40px;
  position: absolute;
  top: 32px;
  right: 20px;
  height: 20px;
  line-height: 20px;
}
</style>