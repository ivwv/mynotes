# align-items和align-content的区别

### 文章目录

- [1. stack overflow上的回答（翻译）](https://juejin.cn/post/6844903911690600456#1_stack_overflow_8)

- [2. 自己动手实践](https://juejin.cn/post/6844903911690600456#2__17)

- - [2.1 子项为单行的情况](https://juejin.cn/post/6844903911690600456#21__18)

  - - [2.1.1 flex容器不设置高度](https://juejin.cn/post/6844903911690600456#211_flex_62)
    - [2.1.2 flex容器设置高度](https://juejin.cn/post/6844903911690600456#212_flex_93)

  - [2.2 子项为多行的情况](https://juejin.cn/post/6844903911690600456#22__127)

  - - [2.2.1 flex容器不设置高度](https://juejin.cn/post/6844903911690600456#221_flex_161)
    - [2.2.2 flex容器设置高度](https://juejin.cn/post/6844903911690600456#222_flex_195)

  - [2.3 补充](https://juejin.cn/post/6844903911690600456#23__232)

- [3. 总结](https://juejin.cn/post/6844903911690600456#3__253)

在用flex布局时，发现有两个属性功能好像有点类似：align-items和align-content，乍看之下，它们都是用于定义flex容器中元素在交叉轴（主轴为flex-deriction定义的方向，默认为row，那么交叉轴跟主轴垂直即为column，反之它们互调，flex基本的概念如下图所示）上的对齐方式，那么它们之间有什么区别呢？

本文通过实例代码来对此展开研究（flex-direction默认为水平方向，环境为google浏览器：版本 72），主要分为三部分：

① 翻译stack overflow的好的回答。

② 自己代码实例展示差别。

③ 总结。

注：本文只限属性取值为center的情况，其他属性值请自己尝试。



# 1. stack overflow上的回答（翻译）

详见问题：[stackoverflow.com/questions/3…](https://link.juejin.cn/?target=https%3A%2F%2Fstackoverflow.com%2Fquestions%2F31250174%2Fcss-flexbox-difference-between-align-items-and-align-content)

- [justfiy-content](https://link.juejin.cn/?target=https%3A%2F%2Fwww.w3.org%2FTR%2Fcss-flexbox-1%2F%23propdef-justify-content)属性可应用于所有的flex容器，它的作用是设置flex子项（flex items）在主轴上的对齐方式。不同取值的效果如下所示：
  ![justify-content](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e33bff5aa6~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
- [align-items](https://link.juejin.cn/?target=https%3A%2F%2Fwww.w3.org%2FTR%2Fcss-flexbox-1%2F%23propdef-align-items)属性可以应用于所有的flex容器，它的作用是设置flex子项在每个flex行的交叉轴上的默认对齐方式。不同取值的效果如下所示：
  ![allign-items](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e33c00797f~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
- [align-content](https://link.juejin.cn/?target=https%3A%2F%2Fwww.w3.org%2FTR%2Fcss-flexbox-1%2F%23propdef-align-content) **只适用**多行的flex容器（也就是flex容器中的子项不止一行时该属性才有效果），它的作用是当flex容器在交叉轴上有多余的空间时，将子项作为一个整体（属性值为：flex-start、flex-end、center时）进行对齐。不同取值的效果如下所示：
  ![align-content](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e33c2b8466~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
  实际上，该说法并不是很准确（见第2.3的例子），以下我们通过实例代码来验证一下。

# 2. 自己动手实践

## 2.1 子项为单行的情况

初始代码（后面例子的代码中省略了与flex无关且不变的部分）如下：

```
<div className='flex'>
     <div className='i1'>1</div>
     <div className='i2'>2</div>
     <div className='i3'>3</div>
     <div className='i4'>4</div>
</div>
复制代码
```

对应的CSS：

```
.flex {
	width: 500px;
	margin: 10px;
	text-align: center;
	border: 2px solid #9a9a9a;
	display: flex; /* 默认的flex-direction为row，则交叉轴方向为column，即垂直方向*/
}
.flex div {
	width: 100px;
	margin: 5px;
}
.i1 {
	background-color: #ffb685;
	height: 130px;
}
.i2 {
	background-color: #fff7b1;
	height: 50px;
	width: 120px;
}
.i3 {
	background-color: #b1ffc8;
	height: 100px;
}
.i4 {
	background-color: #b1ccff;
	height: 60px;
}
复制代码
```

效果如下所示：
![初始状态](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e3532cf5f9~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：在所有的flex布局中，这里其实有浏览器默认的属性：**align-items: normal;** 和 **align-content: normal;**，效果为顶部对齐。

### 2.1.1 flex容器不设置高度

初始状态：

```
.flex {
	display: flex;
}
复制代码
```

效果如下所示：
![单行不设置高度的初始状态](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e3532cf5f9~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：有默认的属性`align-items: normal;`，效果为顶部对齐。

1. 设置 **align-items : center**

```
.flex {
	display: flex;
	align-items: center;
}
复制代码
```

效果如下所示：
![单行不设置高度：align-items: center;](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e3576bab78~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：可以看到容器的高度为最高子项的高度，在一行的所有子项全都在交叉轴上居中对齐，即子项的高度中线与flex交叉轴中线重合。

1. 设置 **align-content: center**

```
.flex {
	display: flex; 
	align-content: center;
}
复制代码
```

效果如下所示：
![单行不设置高度：align-content: center;](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e35e2604b7~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：可以看到与初始状态并没有区别，即在flex容器不设置高度并且子项只有一行时，`align-content`属性是不起作用的。

### 2.1.2 flex容器设置高度

初始状态：

```
.flex {
	height: 500px; /* 给flex容器添加一个高度 */
	display: flex;
}
复制代码
```

效果如下所示：
![单行设置高度](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e36cf76982~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**： 与flex容器不设置高度差不多，只是外层容器的高度增加而已。

1. 设置 **align-items : center**

```
.flex {
	height: 500px;
	display: flex;
	align-items: center;
}
复制代码
```

效果如下所示：
![单行设置高度：align-items: center;](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e380ce4583~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：可以看到在一行的所有子项全都在交叉轴上居中对齐，与flex容器高度不设置时的效果一样（只不过此时高度最大的子项也居中对齐了）。

1. 设置 **align-content: center**

```
.flex {
	display: flex;
	align-content: center;
}
复制代码
```

效果如下所示：
![单行设置高度：align-content: center;](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e380e76950~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：可以看到，此时`align-content: center;`并没有起作用，效果与初始状态一样。

## 2.2 子项为多行的情况

初始状态：

```
<div className='flex'>
     <div className='i1'>1</div>
     <div className='i2'>2</div>
     <div className='i3'>3</div>
     <div className='i4'>4</div>
     <div className='i5'>5</div>
     <div className='i6'>6</div>
</div>
复制代码
```

对应的CSS：

```
.flex {
	width: 500px;
	margin: 10px;
	border: 2px solid #9a9a9a;
	text-align: center;
	display: flex;
	flex-wrap: wrap; /* 使flex容器一行放不下子项换行*/
}
.i5 {
	background-color: #c8b1ff;
	height: 40px;
}
.i6 {
	background-color: #ffb1e5;
	height: 80px;
}
复制代码
```

效果如下所示：
![多行不设置高度的初始状态](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e38902b494~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：同单行一样，这里也有浏览器默认的属性：**align-items: normal;** 和 **align-content: normal;**，效果为顶部对齐。

### 2.2.1 flex容器不设置高度

初始状态：

```
.flex {
	display: flex;
	flex-wrap: wrap; 
}
复制代码
```

效果如下所示：
![多行不设置高度的初始状态](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e38902b494~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：默认顶部对齐，每一行的高度为该行子项中高度最大的那个值。

1. 设置 **align-items : center**

```
.flex {
	display: flex;
	flex-wrap: wrap; 
	align-items: center;
}
复制代码
```

效果如下所示：
![多行不设置高度：align-items : center;](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e394d38b10~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：可以看到各行的子项都在各自行上居中对齐（各行的高度由高度最高的子项决定，flex容器的高度为所有行的高度最高的子项高度之和）。

1. 设置 **align-content: center**

```
.flex {
	display: flex;
	flex-wrap: wrap; 
	align-content: center;
}
复制代码
```

效果如下所示：
![多行不设置高度：align-content: center;](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e3a0c1d80e~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：与初始状态一样，`align-content: center`并没有起作用，因为此时是以所有子项作为一个整体，而flex容器并没有指定高度（flex容器的高度即为子项整体的最大高度），所以flex容器在交叉轴上没有多余的空间，那么子项整体自然而然也就没有在交叉轴上对齐的说法了。

### 2.2.2 flex容器设置高度

初始状态：

```
.flex {
	height: 500px;
	display: flex;
	flex-wrap: wrap; 
}
复制代码
```

效果如下所示：
![多行设置高度初始状态](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e3ac08ce85~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：由浏览器的默认值确定。

1. 设置 **align-items : center**

```
.flex {
	height: 500px;
	display: flex;
	flex-wrap: wrap; 
	align-items: center;
}
复制代码
```

效果如下所示：
![多行设置高度：align-content: center;](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e3bb2a61e9~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：这里我们可以看出，子项分为2行，flex容器将交叉轴上的多余空间按行数平均分给每行，然后每行各自按自己所在的行居中对齐（此时的单行效果跟2.1.2中的例子1效果一样）

1. 设置 **align-content: center**

```
.flex {
	height: 500px;
	display: flex;
	flex-wrap: wrap; 
	align-content: center;
}
复制代码
```

效果如下所示：
![多行设置高度：align-content: center;](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e3c425d8e2~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：我们可以看到，在flex容器指定高度并且子项为多行时，`align-content: center`是将子项作为一个整体，然后这个整体在flex容器的交叉轴上居中对齐的。

## 2.3 补充

以上为什么要区分flex容器是否有固定高度是因为有一种特殊的情况，即：当子项为单行，flex容器具有固定的高度并且设置了`flex-wrap: wrap;`时，`align-content: center;`对单行的子项也有作用。

```
<div className='flex'>
     <div className='i1'>1</div>
     <div className='i2'>2</div>
     <div className='i3'>3</div>
     <div className='i4'>4</div>
</div>
复制代码
.flex {
	height: 500px;
	display: flex;
	flex-wrap: wrap; 
	align-content: center;
}
复制代码
```

效果如下所示：
![单行设置高度，flex-wrap: wrap; align-content: center;](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/13/16c884e3e3fab3a5~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)
**结论**：可以看到此时，`align-content: center;`将单行的子项作为一个整体在交叉轴居中了。

# 3. 总结

如下表：

| 条件     | 属性（是否有效果） |                                           |               |
| -------- | ------------------ | ----------------------------------------- | ------------- |
| 子项     | flex容器           | align-items                               | align-content |
| 单行     | 不指定高度         | 是                                        | 否            |
| 固定高度 | 是                 | 否（但是有设置flex-wrap:wrap;时，有效果） |               |
| 多行     | 不指定高度         | 是                                        | 否            |
| 固定高度 | 是                 | 是                                        |               |

**结论**：从上表可知，对于`align-items`和`align-content`的区别，我们只需要记住以下两点，

1. **align-items属性是针对单独的每一个flex子项起作用，它的基本单位是每一个子项，在所有情况下都有效果（当然要看具体的属性值）。**
2. **align-content属性是将flex子项作为一个整体起作用，它的基本单位是子项构成的行，只在两种情况下有效果：①子项多行且flex容器高度固定 ②子项单行，flex容器高度固定且设置了flex-wrap:wrap;**

这里有个flex布局的小教程，感兴趣的同学可以玩玩：[flexboxfroggy.com/](https://link.juejin.cn/?target=http%3A%2F%2Fflexboxfroggy.com%2F)

注：这里的高度固定的意思实际上是让flex容器在交叉轴上有多余的空间。