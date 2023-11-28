---
title: 一些Css样式整理
date: 2023-11-17 15:08:49
tags: Css
categories: 前端
---

## 文本超出省略号

通过 css 设置文字强制不换行超出用省略号表示:

```css
{
    white-space: nowrap; 文本强制不换行；
    text-overflow:ellipsis; 文本溢出显示省略号；
    overflow:hidden; 溢出的部分隐藏；
}
```

如果要想显示两行超出用省略号表示:

```css
 {
  overflow: hidden;
  -webkit-line-clamp: 2;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-box-orient: vertical;
}
```

## 背景颜色线性渐变

CSS：linear-gradient()背景颜色线性渐变

语法：

`background-image: linear-gradient(direction, color-stop1, color-stop2, ...);`

direction：用角度值指定渐变的方向（或角度）；

color-stop1,color-stop2,...：用于指定渐变的起止颜色

_ps_：至少需要两种颜色

| 方向             | 枚举值    | 角度值 |
| ---------------- | --------- | ------ |
| 从下到上         | to top    | 0deg   |
| 从左到右         | to right  | 90deg  |
| 从上到下（默认） | to bottom | 180deg |
| 从右到左         | to left   | 270deg |

举例：

```css
background: linear-gradient(to right, #feac5e, #c779d0, #4bc0c8);
```

效果如下：

![](/images/example.png)

---

慢慢整理......
