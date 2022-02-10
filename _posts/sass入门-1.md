---
title: sass入门-1
date: 2022-02-10 09:08:43
tags: sass
---
# sass入门
学习自https://juejin.cn/post/6971458017267187719
SCSS,一种 CSS-like 语法
## sass是css的预编译语言，css扩展语言

## 安装sass

```
yarn add sass-loader sass
```

## 编译sass为css
```
sass input.scss ouput.css
```

表示将input.sass编译为output.css

### 监视sass变化并编译
```
sass --watch input.scss:ouput.css
```
表示监视变化，当input.scss一变化，output.css就变化
### 监视文件夹
```
sass --watch yuan:bian
```
表示：当名字为yuan这个文件夹里任意一个.scss后缀的文件变化时，就将其编译到名字bian这个文件夹里面（会自动生成相应的.css文件）

## 基础用法

### 变量
定义一个变量：
```
$yanse:rgb(122,122,122)
```
使用：
```
i{
  color:$yanse;  
}
```
套娃：
```
$yanse:rgb(122,122,122)
$kuang:1px solid $yanse;
```

### 嵌套
例如：
```
div{
    height:100px;
    ul{
        height:80px;
        li{
            height:50px;
        }
    }
}
```
伪类选择器：&:
```
div{ 
    height: 100px; 
    ul{ 
        height: 80px; 
        li{ 
            height: 50px; 
            &:hover {
                color: #000; 
            } 
        } 
    } 
}
```
属性嵌套：
```
div{
    border: 1px solid red {
        left: 0; 
        top: 0; 
    }
}
```
相当于：
```
div {
    border: 1px solid red;
    border-left: 0;
    border-top: 0; 
}
```
## mixin 混入（相当于预先写好了一组样式，其它地方直接引用）
### 基本语法
```
@mixin 名字（参数1，参数2，...） {
    ........样式....... 
}
```
例：
```
@mixin hunhe { 
    color: red; 
    a { 
        font-size: 12px; 
    } 
} 
div{
    @include hunhe; 
}
```
相当于：
```
div { color: red; } 
div a { font-size: 12px; }
```
### 带参数
```
@mixin hunhe($one,$two) { 
    color: $one; 
    a { 
        color: $one; font-size: $two; 
    } 
} 
div{ 
    @include hunhe(red,15px); 
}
```
或：(指定参数名，可以变换参数位置)
```
div{ @include hunhe($two:15px,$one:red); }
```

## 继承/扩展（一个选择器可以继承另一个选择器的全部样式）

例如：
```
.one{
    color: #000;
} 
.one a{ 
    font-size: 10px; 
} 
.two{ 
    @extend .one; 
    background-color: #fff; 
}
```
.two会继承.one的所有样式，包括子代
相当于：
```
.one, .two { 
    color: #000; 
} 
.one a, .two a { 
    font-size: 10px; 
} 
.two {
    background-color: #fff;
}
```
## @import 引入文件
Sass 中 `@import` 指令则可以位于文件中的任意位置。
### 引入scss文件
使用```@import "colors";```引入colors.scss文件

### **使用SCSS部分文件**
当通过`@import`把`scss`样式分散到多个文件时，你通常只想生成少数几个`css`文件。那些专门为`@import`命令而编写的`scss`文件，并不需要生成对应的独立`css`文件，这样的`scss`文件称为局部文件。对此，`sass`有一个特殊的约定来命名这些文件。

即***在文件名前加 _***
注意，此引入的不会生成该文件的css文件
例：
```
@import "themes/night-sky";
```
### 默认变量值
一般情况下，后面的变量值会覆盖前面的变量值
我们可以通过加!default
例如：
有blue.scss文件
```
$link-color: blue !default;
```
我们在文件中导入
```
$link-color: red;
@import 'blue'
```
此时颜色为红色