---
title: Lifecycle hook
date: 2021-03-14
tags:
 - vue 3.0
categories:
 -  Lifecycle hook
---
# 生命周期钩子

> 本指南假定你已经阅读了 [组合式 API 简介]()和[响应性基础]()。如果你不熟悉组合式 API，请先阅读这篇文章。

你可以通过在生命周期钩子前面加上 “on” 来访问组件的生命周期钩子。

下表包含如何在 [setup ()]() 内部调用生命周期钩子：

选项式 API   | Hook inside `setup`
------------- | -------------
`beforeCreate`   |	Not needed*
`created`        |  Not needed*
`beforeMount`    |	`onBeforeMount`
`mounted`        |	`onMounted`
`beforeUpdate`   |	`onBeforeUpdate`
`updated`        |	`onUpdated`
`beforeUnmount`  |	`onBeforeUnmount`
`unmounted`      |	`onUnmounted`
`errorCaptured`  |  `onErrorCaptured`
`renderTracked`  |	`onRenderTracked`
`renderTriggered`|	`onRenderTriggered`

:::tip
**TIP**

因为 `setup` 是围绕 `beforeCreate` 和 `created` 生命周期钩子运行的，所以不需要显式地定义它们。换句话说，在这些钩子中编写的任何代码都应该直接在 `setup` 函数中编写。
:::

这些函数接受一个回调函数，当钩子被组件调用时将会被执行:

```javascript
// MyBook.vue

export default {
  setup() {
    // mounted
    onMounted(() => {
      console.log('Component is mounted!')
    })
  }
}
```