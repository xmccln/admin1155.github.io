---
title: web学习1
date: 2024-10-16 09:00:47
tags: [web前端,笔记,学习]
---

# head

head中通常存放网页的基本信息

```html
<head>
    <!-- 这里面是页面的信息 -->
</head>
```
# meta
meta是确定网页信息的重要标签 

## 字符编码 
**字符编码**的确定可以防止乱码  
常用字符编码为**utf-8**它包含了常用的字符  
可以用如下设置字符编码：
```html
<meta charset = "字符编码样式">
```

# vscode 小技巧
## Emmet快速填充
使用Emmet语句可以快速填充:
* 填充元素
```emmet
h${文本$}*5
```
则填充出来的数据为：
```html
<h1>文本1</h1>
<h2>文本2</h2>
<h3>文本3</h3>
<h4>文本4</h4>
<h5>文本5</h5>
```
* 填充列表
```emmet
ul>li*5
```

则填充的数据为
```html
<ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
</ul>
```