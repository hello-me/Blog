---
title: '关于BFC'
date: 2018-09-17 15:08:32
tags:
---
### BFC(边距重叠解决方案)
#### BFC 的基本概念
块级格式化上下文
#### BFC的原理
 既BFC的布局规则
 1.处于同一BFC中的元素互相影响，可能会发生margin collapse(块级元素的上外边距和下外边距有时会合并（或折叠）为一个外边距，其大小取其中的最大者，这种行为称为外边距折叠)
 2.BFC在页面上是一个独立的容器，容器里面的子元素不会影响到外面，反之亦然
 3.计算BFC的高度时，考虑BFC所包含的所有元素，包含浮动元素也参与计算
 4.浮动盒的区域不会叠加到BFC上
 #### 如何创建BFC
 overflow: 不为visible
 position: absoluted, fixed
 float: 不为none
 display：inline-block\table-cell\table-caption\flex\inline-flex
 BFC使用场景
 1. 防止垂直margin重叠
 父子元素的边界重叠得到解决方案
 在父元素上加上overflow：hidden使其成为BFC
 兄弟元素边界重叠，在第二个子元素创建一个BFC上下文
 2. 清楚内部浮动
 父元素#float的高度为0，解决方案为父元素#float创建BFC，这样浮动子元素的高度也会参与父元素的高度计算
 
 
   