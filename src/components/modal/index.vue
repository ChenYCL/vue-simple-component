<template>
  <div id="modal-root" v-if="modal">
    <div class="modal">
      <div class="box">
        <div class="title">
          {{title}}
        </div>
        <div class="content">
          <div v-if="!$slots.hasOwnProperty('content')">
            {{content}}
          </div>
          <slot v-else name="content"></slot>
        </div>
        <div slot="btn-group" class="btn-group">
          <div class="cancel" @click="cancelEv">取消</div>
          <div class="confirm" @click="confirmEv">确定</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    name: "index",
    data () {
      return {
        modal: false
      }
    },
    props: {
      title: { // 标题
        type: String,
        default: 'Title'
      },
      content: {  // 内容
        type: String,
        default: '敬请期待'
      },
    },
    beforeDestroy () {

    },
    mounted () {

    },
    methods: {
      cancelEv () {
        this.$emit('cancel');
        this.modal = false;
        console.log('---cancel---')
      },
      confirmEv () {
        this.$emit('confirm')
        this.modal = false;
        console.log('---confirm---')

      }
    },
    created () {

    }
  }
</script>

<style scoped lang="scss">
  // modal
  #modal-root {
    position: relative;
    z-index: 999;
  }

  .modal {
    background-color: rgba(18,18,18,0.5);
    position: fixed;
    height: 100%;
    width: 100%;
    top: 0;
    left: 0;
    display: flex;
    align-items: center;
    justify-content: center;


    .box {
      width: calc(100% / 750 * (750 - 120));
      background: #272E73;
      padding: {
        left: 20px;
        right: 20px;
        bottom: 30px;
      };

      .title {
        font-size: 18px;
        font-weight: 500;
        color: white;
        text-align: center;
        padding-top: 30px;
      }

      .content {
        font-weight: 400;
        text-align: center;
        color: rgba(255, 255, 255, 0.1);
        padding: {
          top: 30px;
          bottom: 30px;
        };
      }

      .btn-group {
        display: flex;
        flex-direction: row;
        width: 100%;
        text-align: center;
        font-size: 16px;
        font-weight: 500;
        align-items: center;
        .cancel {
          flex: 1;
          border: 1px solid #2AB3FF;
          padding: 14px 0;
          color: #2AB3FF;
        }

        .confirm {
          flex: 1;
          padding: 14px 0;
          color: white;
          background: linear-gradient(to right, #2AB3FF, rgb(34, 47, 250));
          margin-left: 10px;

        }

      }
    }
  }

</style>