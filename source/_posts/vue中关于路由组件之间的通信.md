---
title: vue中关于路由组件之间的通信
date: 2018-04-28 17:10:30
tags:
---
偶然一次使用vue开发项目时，有一个业务场景是这样的

header组件中 有一个搜索框，输入关键字搜索时，不论那个页面

都会跳转到list页面，同时list页面重新加载数据 

## 一、使用bus监听
**header.vue**

```
this.$emit('search', this.key)
```

**list.vue**

```
this.$on('search', key => {
    consoe.log(key)
})
```

实践证明 在list.vue中根本触发不了不了 search 事件

扑街

## 二、使用vuex
**header.vue**

关键代码如下
```
import {mapMutaions} from 'vuex
...

methods: {
    ...mapMutaions(['updateKey']),
    search () {
        this.updateKey(this.key)
    }
}

```

**list.vue**

```
this.$on('search', key => {
    consoe.log(key)
})
```