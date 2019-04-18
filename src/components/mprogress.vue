<template>
    <section>
        <div class="wrapper" :style="`height:${height}px;width:${width}px;display:block;background:${color}`">
            <span class="val" :style="`background:${innercolor};width:${(value/max)*width}px;`"></span>
        </div>
    </section>
</template>

<script>
  export default {
    name: "mprogress",
    props:{
      color:{
        type:String,
        default:'#CCD0D3'
      },
      value:{
        type:Number|String,
        default: 50
      },
      max:{
        type:Number,
        default:100
      },
      height:{
        type:String|Number,
        default:'2'
      },
      width:{
        type:String|Number,
        default:'25'
      },
      innercolor:{
        type:String,
        default:' #0CBA71'
      }
    }
  }
</script>

<style scoped lang="scss">
    .wrapper{
        border-radius: 20px;
        position: relative;
        overflow: hidden;
        .val{
            display: inline-block;
            position: absolute;
            z-index: 1;
            height: 100%;
            top:0;
            left: 0;
            border-radius: 20px;
        }
    }
</style>