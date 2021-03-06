# h5-template

用于进行h5活动开发的框架，主要用于解决静态资源的打包和加载以及本地环境和线上环境的调试。

## 环境

```
node v8.5.0
npm v.5.3.0
```

```
webpack v3.7.1
```

## 目录说明

~~~
├── dist（打包后目录）
├── src（源码目录）
│   ├── assets（公共js、css、图片等资源）
│   ├── pages（活动页面，每个单独活动为一个文件夹）
├── .csscomb.json 样式格式化配置文件
├── .eslint.js js格式化配置文件
├── webpack.common.js webpack公共配置文件
├── webpack.dev.js webpack开发环境配置文件
├── webpack.prod.js webpack正式环境配置文件
~~~

## 待解决问题

* html修改自动刷新
* 修改 ```webpack``` 配置文件自动重启服务
* 图片不上传至代码库而是在本地调试时上传至图片cdn

## 如何使用

项目的入口文件分为三个部分 ```head.js``` ```vendors.js``` 以及 ```[page].js```，在 ```html``` 中引入时使用统一的路径前缀 ```/publics/[name].js```

```head.js``` 用于在 ```<head></head>``` 标签中引入的js文件，目前打包了下列三个文件。

* ```flexible.js``` 移动端rem适配方案
* ```gio.js``` growingio数据采集
* ```zhanzhang.js``` 百度站长统计

```vendors.js``` 为项目的公共js文件，目前打包了下列两个文件。

* ```common.js``` 公共方法以及工具方法
* ```rela.js``` 和客户端通讯的相关方法

```vendors.css``` 为项目的公共css文件，目前打包了下列两个文件。

* ```reset.scss```
* ```normalize.css```

```[page].js``` 为当前活动名称的js文件，文件名与活动名一致。

### 创建活动

1. 在 ```pages``` 文件夹下创建一个以活动名称命名的文件夹 ```/demo```，活动相关的所有静态资源全部存放在当前文件夹下。

2. 在 ```/demo``` 文件夹下创建 ```index.html``` 并引入 ```head.js``` ```vendors.js``` 和 ```vendors.css``` 默认当前三个文件都需要在每个活动中引入，视具体需求选择。

```html
// index.html
<html>
  <head>
    <title>测试</title>
    <script src="/publics/head.js"></script>
    <link rel="stylesheet" href="/publics/vendors.css" />
  </head>
  <body>
    <script src="/publics/vendors.js"></script>
  </body>
</html>
```

3. 创建 ```index.js``` 和 ```index.scss```

```js
// 引入的scss文件才会被编译
import './index.scss';

alert('demo.js');
```

```scss
h1{
  color: red;
}
```

4. 在 ```html``` 中引入编译好的静态资源

```html
<html>
  <head>
    <title>测试</title>
    <script src="/publics/head.js"></script>
    <link rel="stylesheet" href="/publics/vendors.css" />
    <link rel="stylesheet" href="/publics/demo.css" />
  </head>
  <body>
    <h1>demo</h1>
    <script src="/publics/vendors.js"></script>
    <script src="/publics/demo.js"></script>
  </body>
</html>
```

5. 执行以下命令重启项目，就可以进行后续的开发和调试了
```js
npm run dev
```


