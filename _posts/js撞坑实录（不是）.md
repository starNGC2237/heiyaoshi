---
title: js撞坑实录（不是）
date: 2022-1-30 14:18:06
tags: javascript
---
## 浮点数计算问题
### 关于浮点数加减乘除不对

```js
const a =0.1+0.2
a = 0.30000000000000004 !=0.3
```
是底层的计算问题

解决方法：

- 使用库 Math.js
[官网](https://link.zhihu.com/?target=http%3A//mathjs.org/)

[GitHub](https://link.zhihu.com/?target=https%3A//github.com/josdejong/mathjs)

- 使用toFixed()方法
该方法使用定点表示法来格式化一个数，会对结果进行四舍五入。
```js
numObj.toFixed(digits)
```
参数digits表示小数点后数字的个数；介于 0 到 20 （包括）之间，实现环境可能支持更大范围。如果忽略该参数，则默认为 0。

**但是！ 此方法返回值为String**

例如：
```js
const a =0.1+0.2
a.toFixed(10) == 0.3
```


## 拷贝问题
### 拷贝对象
```
// 为什么要克隆（因为js中相等是将对象地址相等
// 克隆对象的方法：
// loash的方法(一般使用) _.cloneDeep(value)（深拷贝）（和递归一样）
// 递归查找至基础数据类型
// 转为string再转回来 （undefined、function、symbol 会在转换过程中被忽略）
// es6语法 const a={...b} 如果其中有对象（例如b:{a:1}），对象b转换后依然是原地址（即a与b的b指向同一个）
```