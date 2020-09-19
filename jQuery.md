#### .val

![image-20200327103517659](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200327103517659.png)

#### .find 

![image-20200327103640942](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200327103640942.png)

#### for in 

![image-20200327104344589](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200327104344589.png)

#### .html

![image-20200327104726231](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200327104726231.png)

### Juicer

Juicer 是一个高效、轻量的前端 (Javascript) 模板引擎，使用 Juicer 可以是你的代码实现数据和视图模型的分离(MVC)。除此之外，它还可以在 Node.js 环境中运行。

<script type="text/javascript" src="juicer-min.js"></script>

## * 使用方法

\> 编译模板并根据所给的数据立即渲染出结果.

```

juicer(tpl, data);
```

#### c. 循环遍历 {@each} ... {@/each}

如果你需要对数组进行循环遍历的操作，就可以像这样使用 `each` .

```

{@each list as item}	${item.prop}{@/each}
```



如果遍历过程中想取得当前的索引值，也很方便.

```

{@each list as item, index}	${item.prop}	${index} //当前索引{@/each}
```

#### . 判断 {@if} ... {@else if} ... {@else} ... {@/if}

我们也会经常碰到对数据进行逻辑判断的时候.

```

{@each list as item,index}    {@if index===3}        the index is 3, the value is ${item.prop}    {@else if index === 4}        the index is 4, the value is ${item.prop}    {@else}        the index is not 3, the value is ${item.prop}    {@/if}{@/each}
```

#### .attr

![image-20200327111741223](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200327111741223.png)