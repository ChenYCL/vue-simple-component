# vue-simple-conponent

## 依赖安装
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

# 组件
### 头部标题栏 
-------
```JavaScript

 /**
   * 引用方式 
   *   <t-nav r-color="red" r-text="记录" left-icon="bg.png" :left-show="true" :right-icon="require('../../assets/images/home_c2c_press.svg')" :back-func="func1" :right-ev="func2" title="首页1"></t-nav>
        
        
        增加<slot name="rightContent"></slot> 插槽，覆盖右侧部分配置
   */
   
   props: {
      color:{ // 背景色
        type:String,
        default:''
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
      rightIcon: { // 右侧图标地址
        type: String,
        default: ''
      },
      backFunc: { // 左侧event 默认返回路由上级，覆盖事件不进行任何操作 :back-func="()=>{}" 覆盖
        type: Function,
        default: null
      },
      rColor:{ // 右侧文字颜色
        type:String,
        default:''
      },
      rText:{ // 右侧文字
        type:String,
        default:''
      },
      rightEv: { // 右侧event
        type: Function,
        default: () => {
          return null
        }
      }
      
      
```
### t-bar
-------
```JavaScript
 /** eg.
   *  <t-bar :h="10" color='red'/> 
   */
   
   props:{
      color:{ // 背景色
        type:String,
        default:styles.base7
      },
      h:{// 高度
        type: Number,
        default: 10
      }
    }

```

### 弹窗 modal
```JavaScript
    e.g 默认
  
     <modal title="标题" ref="$toast"  :content="我是内容文字"></modal>
 
    
    e.g 插槽
       
    <modal title="标题" ref="$toast" @cancel="cancel事件" @confirm="confirm事件">
      <div slot="content">
        <h2>Hello</h2>
      </div>
    </modal>
    
    // 显示 this.$refs.$toast.modal = true;
    // 销毁 this.$refs.$toast.modal = fale;
```

## 列表 t-list


```JavaScript

e.g:
 
  // 默认样式  回调函数ev，获取当前点击内容

  <div class="content" style="display: flex" >
    <t-list @ev="h"></t-list>
    <t-list></t-list>
    <t-list></t-list>
    <t-list></t-list>
  </div>
      
    methods:{ 
      h(data){
        console.log(data);
      }
    }


// 自定义内部样式  demo
      <t-list title=""  :data="[1,'test',3,4,5]" :border-bottom="true">
          <div :slot="key" v-for="(item,key) in [1,'test',3,4,5]" :key="key">
            <h1 style="color: red">{{item}}</h1>
            <p>2018-10-10</p>
          </div>
      </t-list>
  
  
  组件属性
  
    column:{  // 列表排列 默认竖向
        type:Boolean,
        default:()=>{
          return true
        }
      },
      wrapper:{ // 容器样式 可选 css插入覆盖 const style = `height:10px...`
        style:String,
        defalut: ''
      },
      top:{ // 内容 padding-top
        type:Number,
        default:15
      },
      bottom:{ // 内容 paddint-bottom
        type:Number,
        default:15
      },
      title: {  // 顶部标题
        type: String,
        default: () => {
          return "收益"
        }
      },
      width: { // 列表宽度 单位%
        type: Number,
        default: 100
      },
      data: { // 渲染数据
        type: Array,
        default: () => {
          return [
            1, 2, 3, 4, 5, 6, 7, 8
          ]
        }
      },
      borderBottom:{ // 列表下边框显示控制
        type:Boolean,
        default:true
      },
      ulStyle:{ // ul 内联样式
        type:String,
        default: ''
      }
```

## bootom-sheet
```JavaScript
    e.g 默认
    <sheet ref="sheet" :data=["1","2","3"] @select="choose" @confirm="sheetChoose"/>
    
    e.g 对象取值
     <sheet ref="sheet" :data="[{coin:'btc'},{coin:'bch'}]" _key="coin"  @select="choose" @confirm="sheetChoose" />
    
    // 回调形参为接收值 select 选中 || confirm 确定
    
    choose(feedback){
       console.log(feedback)
    }
     
     
    // 激活/销毁
    $refs.sheet.show=true/false
```

<table>
    <thead>
    <tr>
        <th width="180">组件名称</th>
        <th width="320">组件路径</th>
        <th width="180">备注</th>
    </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="#fontStyle" >radio组件</a></td>
            <td>src/components/radio/radio.vue</td>
            <td>radio组件</td>
        </tr>
        <tr>
            <td><a href="#fontStyle" >msg组件</a></td>
            <td>src/components/message/index.vue</td>
            <td>msg组件</td>
        </tr>
    </tbody>
</table>


##  radio组件使用


```
<teTradio v-model="radio" value="1" @change="onChange">radio1</teTradio>
<teTradio v-model="radio" value="2" @change="onChange">radio2</teTradio>

```

回调函数：
     data(){
         return {
            radio:0
         }
     },
     
     method: {
        onChange(val){
            console.log(val); // 选中的返回值
         }
     }
 



####  参数说明


<table>
    <thead>
    <tr>
        <th width="180">参数</th>
        <th width="320">类型/</th>
        <th width="180">说明</th>
    </tr>
    </thead>
    <tbody>
        <tr>
            <td>v-model</td>
            <td>String</td>
            <td>绑定的数据值</td>
        </tr>
        <tr>
            <td>value</td>
            <td>String</td>
            <td>选中radio的值</td>
        </tr>
        <tr>
            <td>change</td>
            <td>function</td>
            <td>回调函数，选中返回的value值</td>
        </tr>
    </tbody>
</table>


#####  msg组件使用

```
this.$message({
    msg: 'test',
    duration: 3000, //可选参数
});
```
