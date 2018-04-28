#《css-secrets》

# 多重边框

> 关键字：边框;box-shadow;outline

## 需求描述

* 实现如下多重边框效果（白色区域无需考虑）

![最终效果.png](https://upload-images.jianshu.io/upload_images/4869616-75f9c4140c4b71cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)

## 常规思路

1.  叠 div
2.  border-image

不好意思，打扰了。。。

## 解决方法

### 方法一：box-shadow

#### 语法

```css
box-shadow: h-shadow v-shadow blur spread color inset;
```

#### 说明

boxShadow 属性把一个或多个下拉阴影添加到框上。该属性是一个用逗号分隔阴影的**列表**，每个阴影由 2-4 个长度值、一个可选的颜色值和一个可选的 inset 关键字来规定。省略长度的值是 0。

| 值       | 说明                                                |
| -------- | --------------------------------------------------- |
| h-shadow | 必需的。水平阴影的位置。允许负值                    |
| v-shadow | 必需的。垂直阴影的位置。允许负值                    |
| blur     | 可选。模糊距离                                      |
| spread   | 可选。阴影的大小                                    |
| color    | 可选。阴影的颜色。在 CSS 颜色值寻找颜色值的完整列表 |
| inset    | 可选。从外层的阴影（开始时）改变阴影内侧阴影        |

#### 实现

叠加`box-shadow`，将水平阴影的位置/垂直阴影的位置/模糊距离置于 0 即可模拟出实现边框效果

```css
#example-box {
  background-color: burlywood;
  box-shadow: 0 0 0 10px brown, 0 0 0 15px aquamarine, 0 0 0 25px pink;
}
```

![最终效果.png](https://upload-images.jianshu.io/upload_images/4869616-75f9c4140c4b71cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)

#### 注意：

1.  宽度是叠加的，也就是说第一道边框宽度是 10px 的话，倘若第二道边框为 5px，那么其阴影大小为 15px

#### 弊端：

1.  无法实现虚线效果
2.  模拟出来的边框不属于盒模型内部区域，即不受到 box-sizing 属性影响，无法触发相应事件(click,hover)，需要通过内外边距进行调整
3.  同上，不会影响布局，需要通过内外边距进行调整

### 方法二：outline(仅限于两层边框的条件下)

#### 语法

```css
outline: #00ff00 dotted thick;
```

#### 说明

outline（轮廓）是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。

outline 简写属性在一个声明中设置所有的轮廓属性。

可以设置的属性分别是（按顺序）：outline-color, outline-style, outline-width

如果不设置其中的某个值，也不会出问题，比如 outline:solid #ff0000; 也是允许的。

#### 实现（两层）

```css
#example-box2 {
  background-color: burlywood;
  border: 10px solid brown;
  outline: 5px solid aquamarine;
}
```

![两重边框.png](https://upload-images.jianshu.io/upload_images/4869616-a6a6079bf3ae8d26.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)

#### 弊端：

1.  模拟出来的边框不属于盒模型内部区域，即不受到`box-sizing`属性影响，无法触发相应事件(click,hover)，需要通过内外边距进行调整
2.  同上，不会影响布局，需要通过内外边距进行调整
3.  不贴合圆角(想想讨厌的圆角 button 点击的时候 outline 总是不解风情)
4.  只能实现两层边框

#### 好处：

1.  可以实现虚线效果
2.  虚线结合 outline-offset 负值实现缝边效果

![缝边效果.png](https://upload-images.jianshu.io/upload_images/4869616-5c3b68656c33f349.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)
