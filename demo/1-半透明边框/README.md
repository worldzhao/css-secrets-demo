#《css-secrets》

# 半透明边框

> 关键字：半透明;边框;background-clip

## 需求描述

* 给一个容器设置一层白色背景和一道半透明白色边框
* body 的背景会从它的半透明边框透上来

![最终效果.png](https://upload-images.jianshu.io/upload_images/4869616-9aa99dbfb7bb5b1c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)

## 常规思路

```css
body {
  background-color: aquamarine;
}

#example-box {
  background-color: #fff;
  border: 10px solid rgba(255, 255, 255, 0.5);
  width: 200px;
  height: 200px;
}
```

## 结果

检查元素，边框确实存在，但是直接是白色，body 并没有从半透明边框透上来

![实际效果.png](https://upload-images.jianshu.io/upload_images/4869616-e57c1824134156f1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)

![检查元素-1.png](https://upload-images.jianshu.io/upload_images/4869616-8a3806f152e8291c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)

![检查元素-2.png](https://upload-images.jianshu.io/upload_images/4869616-3cd81a5ba156e162.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)

## 原因

默认情况下， 背景会延伸到边框所在的区域下层，即`#example-box`的白色背景延伸到了半透明边框下

使用黑色虚线边框进行测试

```css
border: 10px dashed #000;
```

如图所示

![测试.png](https://upload-images.jianshu.io/upload_images/4869616-2b3330e5bd68b65d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)

可见虚线之间都是`#example-box`的白色背景部分

## 解决方法

background-clip
作用：裁剪元素背景

```css
body {
  background-color: aquamarine;
}

#example-box {
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid rgba(255, 255, 255, 0.5);
  width: 100px;
  height: 100px;
}
```

![最终效果.png](https://upload-images.jianshu.io/upload_images/4869616-9aa99dbfb7bb5b1c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)
