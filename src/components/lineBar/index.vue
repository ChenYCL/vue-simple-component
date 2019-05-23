<template>
  <div :style="`background:${color};height: ${h}px;`"></div>
</template>

<script>
  /**
   *  <t-bar h=10 color='red'/>
   */
  export default {
    name: "index",
    props:{
      color:{ // 背景色
        type:String,
        default:'rgba(0, 0, 0, .1)'
      },
      h:{// 高度
        type: Number||String,
        default: 10
      }
    }
  }
</script>

<style scoped lang="scss">

</style>