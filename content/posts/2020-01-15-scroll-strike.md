---
title: 滑动穿透（遮罩下不允许滑动）
date: 2020-01-15 20:31:00
tags: ["CSS"]
---

滑动穿透

<!--more-->

## 情况列举

1. body 无滚动，弹层无滚动
2. body 无滚动，弹层有滚动
3. body 有滚动，弹层无滚动
4. body 有滚动，弹层有滚动

### body 无滚动，弹层无滚动

弹层出现时，body 置为超出隐藏，固定布局，弹层关闭后恢复

打开弹层

```js
layer.style.display = "block";
document.body.style.overflow = "hidden";
document.body.style.position = "fixed"; // 【弊端】因为加了fixed，就会自动回滚到顶部
```

关闭弹层

```js
layer.style.display = "none";
document.body.style.overflow = "auto";
document.body.style.position = "static";
```

#### 问题

用户在超出一屏高度的位置点开弹层，页面会因为 fixed 布局回到顶部

#### 解决

可使用 swiper 控制页面一页一屏

### body 无滚动，弹层有滚动

弹层出现时，body 置为超出隐藏，固定布局，样式中增加允许滑动，弹层关闭后恢复

打开弹层

```js
layer.style.display = "block";
document.body.style.overflow = "hidden";
document.body.style.position = "fixed"; // 【弊端】因为加了fixed，就会自动回滚到顶部
```

```css
overflow-y: scroll;
-webkit-overflow-scrolling: touch; /* 解决在IOS上滚动惯性失效的问题 */
```

关闭弹层

```js
layer.style.display = "none";
document.body.style.overflow = "auto";
document.body.style.position = "static";
```

#### 问题

滑动到页面顶部或底部时仍会发生穿透

#### 解决

当滑动到边界时禁止滑动

### body 有滚动，弹层无滚动

阻止弹层的 touchmove 事件默认行为

### body 有滚动，弹层有滚动

检测 touchmove 事件，如果 touch 的目标是弹窗不可滚动区域（背景蒙层）就禁掉默认事件，反之就不做控制

## 参考

- [滚动穿透的 6 种解决方案【已自测】](https://www.cnblogs.com/padding1015/p/10568070.html)
