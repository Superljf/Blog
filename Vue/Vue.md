### Vue项目搭建

- cnpm i -g vue-cli

- vue init webpack

- cnpm i 

- npm run dev

  #### 可视化构建工具

- cnpm install -g @vue/cli 

- vue ui 

### 公有Vue过滤器进行时间格式化

```js
Vue.filter('dateFormat', function (dateStr, pattern = "" // 这里解决的是当参数为undifinded报错
                                   ){
    var dt - new Date(dateStr)
    var y = dt.getFullYear()
    var m = dt.getMonth() + 1
    var d = dt.getDate()
    
    if (pattern.toLowerCase() === 'yyy-mm-dd') {
        return `${y}-${m}-${d}`
    } else {
        var hh = dt.getHours()
        var mm = dt.getMinutes()
        var ss = dt.getSeconds()

        return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
    }
})
```

### 自定义全局按键修饰符

```js
 // 自定义全局按键修饰符
    Vue.config.keyCodes.f2 = 113
```

### 自定义指令

```js
 <div id="app2">
    <h3 v-color="'pink'" v-fontweight="900" v-fontsize="50">{{ dt | dateFormat }}</h3>
  </div>

  directives: { // 自定义私有指令
        'fontweight': { // 设置字体粗细的
          bind: function (el, binding) {
            el.style.fontWeight = binding.value
          }
        },
        'fontsize': function (el, binding) { // 注意：这个 function 等同于 把 代码写到了 bind 和 update 中去
          el.style.fontSize = parseInt(binding.value) + 'px'
        }
      }


 // 自定义一个 设置字体颜色的 指令
    Vue.directive('color', {
      // 样式，只要通过指令绑定给了元素，不管这个元素有没有被插入到页面中去，这个元素肯定有了一个内联的样式
      // 将来元素肯定会显示到页面中，这时候，浏览器的渲染引擎必然会解析样式，应用给这个元素
      bind: function (el, binding) {
        // el.style.color = 'red'
        // console.log(binding.name)
        // 和样式相关的操作，一般都可以在 bind 执行

        // console.log(binding.value)
        // console.log(binding.expression)

        el.style.color = binding.value
      }
    })
```

### Vue-router的安装

安装 npm install vue-router --save-dev 

### 

### 给URL添加id

```
path: "/blog/:id",
```

- 接收路由参数：  **this**.$route.params.路由参数



#### router.push 

![image-20200330110804730](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200330110804730.png)