---
title: 继承UI组件的属性和方法
date: 2022-09-14 17:24:11
permalink: /pages/dcebaf/
titleTag: 原创
sticky: 1
categories: 
  - 更多
  - 实用技巧
tags: 
  - JavaScript
  - css
  - 实用技巧
author: 
  name: gengbingbing
  link: https://github.com/gengbingbing
sidebar: auto
---

> 如何快速优雅的封装一个第三方组件库的组件呢？v-bind="attrs"和v−on="attrs" 和 v-on="attrs"和v−on="listeners" ="$listeners"，会给我们带来惊喜。它们可以使得封装后的组件， “继承”原组件的几乎所有 v-bind 属性和 v-on 事件，且用法和作用与在原组件一样。

**关键点主要有两个，v-bind和v-on**

## 1、v-bind="$attrs"

v-bind="$attrs"的妙用是在创建更高级别的组件，在封装第三方组件时，可以自动将在父作用域中使用的v-bind的属性自动绑定，并向下传入被封装的使用了v-bind="$attrs"的组件。

## 2、v-on="$listeners"

v-on="listeners"的作用和用法与v−bind="listeners"的作用和用法与v-bind="listeners"的作用和用法与v−bind="attrs"类似，可以将父作用域中的使用v-on的时间监听器向下传入到使用了v-on="listeners"组件中，和v−bind="listeners"组件中， 和v-bind="listeners"组件中，和v−bind="attrs"的功效类似，只不过一个属性一个是事件

## 3、$attrs和props的区别

- props 是父类向子类传递并且需要子类主动接收的属性，当然props不包含事件；

- $attrs 默认是父类传递到子类根元素的属性，子类不用主动接收，会直接放在子类根元素上。 而$attrs 的这种默认行为，可以通过设置inheritAttrs:false，这些默认行为将会被取

  

demo：

```
<custom-Image fit="fill" class="icon-img" :src="picPreview(expert)"></custom-Image>
<template>
  <div id="CustomImage">
    <el-image v-bind="$attrs" v-on="$listeners">
      <div slot="error" class="image-slot">
        <img :src="require('image-f/icon-empty-img.png')" alt="图片加载失败.png"/>
      </div>
      <div slot="placeholder" class="placeholder-slot">加载中...</div>
    </el-image>
  </div>
</template>

<script>
export default {
  name: 'CustomImage'
}
</script>
<style scoped lang="scss">
  #CustomImage {
  .image-slot {
    text-align: center;
  }
  .placeholder-slot {
    text-align: center;
  }
}
</style>
```
