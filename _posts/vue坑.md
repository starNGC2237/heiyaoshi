---
title: vue中遇到的坑
date: 2021-11-20 12:26:37
tags: vue
categories: 
- vue
feature: true
---

# vue中遇到的坑

## vscode 编写中的

### Already included file name ‘×××‘ differs from file name ‘×××‘ only in casing.

vs code的bug

```
快捷键：Ctrl + shift + P，打开：“命令面板”，输入：重新加载
```

如果控制台报错

```cmd
yarn serve
```

## vue生命周期

### 各个生命周期钩子是同步的

意味着：

> created和mounted是同步的

即：

先执行created里的同步代码，再执行mounted里的同步代码，再执行created里的异步代码，再执行mounted里的异步代码



## vue组件与子组件生命周期

beforeCreated

created

beforeMount

 子组件beforeCreated

 子组件created

 子组件beforeMount

 子组件mounted

mouted


