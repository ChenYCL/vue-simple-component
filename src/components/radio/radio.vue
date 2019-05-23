<template>
    <label class="radio-box" :class="{'checked':value==modelValue,'disabled':disabled}">
        <input type="radio" ref="radio" :value="value"  @click="radioEvent($event)" :disabled="disabled">
        <span class="radio-inner"></span>
        <span class="radio-text"><slot/></span>
    </label>
</template>
<script>
    export default {
        name:"tet-radio",
        model: {
            prop: 'modelValue',
            event: 'change'
        },
        props:{
            modelValue:{
                type:[String,Number],
                require:true
            },
            disabled:{
                type:Boolean,
                default:false,
            },
            value:{
                type:[Number,String],
                require:true
            },
        },
        data(){
            return{

            }
        },
        computed:{
        
        },
        created(){
        
        },
        mounted(){

        },
        methods:{
            radioEvent(e){
                this.$emit('change',e.target.value);
            }
        },
    }
</script>
<style scoped lang='scss'>
    .radio-box{
        display: inline-block;
        position: relative;
        input{
            display: none;
            outline: none;
        }
        span{
            display: inline-block;
            vertical-align: middle;
        }
        .radio-inner{
            height: 13px;
            width: 13px;
            border: 1px solid #8286a5;
            border-radius: 50%;
        }
        .radio-text{
            font-size: 13px;
            line-height: 13px;
            padding-left: 10px;
            color: #7582CE;
        }
        &.checked{
            .radio-inner{
                border: none;
                background: url('../../assets/radio_checked.png') no-repeat center /100% 100%;
            }
            .radio-text{
                color: #2AB3FF;
            }
        }
        &.disabled{
            cursor: not-allowed;
        }
    }
</style>