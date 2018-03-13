---
title: 你所不知道的css3动画
date: 2018-02-02 06:14:24
tags: 动画
categories: css3
comments: true
---
## css3 transition
语法 transition: property duration timing-function delay;
如
```css
transition: width 1s ease-in 2s;
```
<!-- more -->
## aniamtion
语法 animation: name duration timing-function delay iteration-count direction fill-mode play-state; 其中fill-mode表示动画不播放时显示的样式效果。
```css
animation: move 1s ease 2s  infinite alterantive
```
## GPU硬件加速
浏览器一般会将文档中的标签解析为DOM树，对于height top等属性运用css3动画时，这时浏览器会发生repaint-重绘，有时你的动画可能出现卡顿的现象，这时可以通过css3的一些属性打开硬件加速。

比如使用css3属性的transform: translate3d(0,0,0),可以打开GPU模式来绘图，这种方式可以使动画更流畅。

## animation中的贝塞尔曲线

## animation中的逐帧动画

## transform的matrix

## 监听transform动画的事件

<iframe height="265" scrolling="no" title="Gravity Points" src="//codepen.io/china-boy/embed/preview/BpjbRK/?height=265&amp;theme-id=0&amp;default-tab=result&amp;embed-version=2" frameborder="no" allowtransparency="true" allowfullscreen="true" style="width: 100%;"><iframe>


<iframe height="365" scrolling="no" title="Gravity Points" src="https://ppt.baomitu.com/embed/5085b233?style=dark" frameborder="no" allowtransparency="true" allowfullscreen="true" style="width: 100%;" webkitallowfullscreen mozallowfullscreen allowfullscreen><iframe>


<!-- <iframe src="https://ppt.baomitu.com/embed/5085b233?style=dark" width="576" height="420" scrolling="no" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen  style="width: 100%;"></iframe> -->
