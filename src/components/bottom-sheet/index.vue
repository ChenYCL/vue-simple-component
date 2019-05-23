<template>
  <div class="bottom-sheet" v-if="visible">
    <div class="sheet-overlay"></div>
    <div class="sheet-container">
      <div class="sheet"
           :class="{'active': item.active}"
           v-for="(item, index) in list"
           :key="index"
           @click="selectItem(item)">
        {{item.value}}
        <div class="divider-horizontal"></div>
      </div>
      <div class="button" @click="handleClose">取消</div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      list: null,
      visible: {
        type: Boolean,
        default: false
      },
    },
    methods: {
      selectItem (item) {
        this.$emit('select', item)
      },
      handleClose () {
        this.$emit('update:visible', false);
        this.$emit('close');
      }
    }
  }
</script>

<style lang="scss" scoped>
  .bottom-sheet {
    .sheet-overlay {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      pointer-events: none;

      &::before {
        background-color: #212121;
        bottom: 0;
        content: '';
        height: 100%;
        left: 0;
        opacity: 0;
        position: absolute;
        right: 0;
        top: 0;
        transition: inherit;
        transition-delay: 150ms;
        width: 100%;
        opacity: 0.46;
      }
    }

    .sheet-container {
      position: fixed;
      width: 100%;
      background-color: $base1;
      color: #FFFFFF;
      transition: 0.3s cubic-bezier(0.25, 0.8, 0.5, 1);
      font-size: 13px;
      text-align: center;
      bottom: 0;

      .sheet {
        height: 46px;
        line-height: 46px;
        position: relative;
      }

      .active {
        color: $base3;
      }

      .button {
        height: 46px;
        line-height: 46px;
        color: $base3;
      }
    }

  }
</style>

