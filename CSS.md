#### 给按钮添加阴影

![image-20200911105849015](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200911105849015.png)

![image-20200911105908203](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200911105908203.png)

```css
html {
    /* 定义变量 */
    --bgColor: #ff5353;

    /* rgba的四个值分别为：红(R)、绿(G)、蓝(B)、透明度(A) */
    --whiteShadow: -15px -15px 25px rgba(255, 117, 117, .5);
    --blackShadow: 15px 15px 25px rgba(110, 40, 40, .2);
}

/* 设置一些页面的布局样式 */
body {
    display: flex;
    margin: 0;
    padding: 0;
    width: 100vw;
    height: 100vh;
    justify-content: center;
    align-items: center;
    background-color: var(--bgColor);
}

.card {
    width: 30vh;
    height: 30vh;
    margin: 45px;
    background-color: var(--bgColor);
    border-radius: 30px;
}

/* 主要部分 */
.left {
    /* 设置外阴影 */
    box-shadow: var(--blackShadow),
                var(--whiteShadow);
}

.right {
    /* 设置内阴影 */
    box-shadow: inset var(--blackShadow),
                inset var(--whiteShadow);
}
```

#### 实现垂直居中

- flex

  ```css
  <style type="text/css">
    .out{
      display: flex;
      justify-content: center;
      align-items: center;
      width: 300px;
      height: 300px;
      background: red;
    }
  
    .inner{
      background: yellow;
      width: 100px;
      height: 100px;
    }
  </style>
  
  
  ```
  
  - grid
  
    父元素指定子元素的对齐方式
  
    ```css
    <style type="text/css">
      .out{
        display: grid;
        align-content: center;
        justify-content: center;
        width: 300px;
        height: 300px;
        background: red;
      }
    
      .inner{
        background: yellow;
        width: 100px;
        height: 100px;
      }
    </style>
    
    ```
  
    子元素自己指定自己的对齐方式
  
    ```css
    <style type="text/css">
      .out{
        display: grid;
        width: 300px;
        height: 300px;
        background: red;
      }
    
      .inner{
        background: yellow;
        width: 100px;
        height: 100px;
        align-self: center;
        justify-self: center;
      }
    </style>
    ```
  
    

