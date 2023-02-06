
### 问题：使用k-form-design后在ie浏览器打开，出现属性不支持等问题

环境：vue cli3以上版本搭建的项目

> 注：由于富文本使用了vue-quill-editor，vue-quill-editor在IE11以下的浏览器会报错，所以就算使用babel/polyfill也只能兼容 IE11

### Installation

```
npm install babel/polyfill --save
# or
yarn add babel/polyfill
```

### `main.js`文件（项目入口）

```js
// 在顶部引入@babel/polyfill处理兼容,以确保首先加载polyfill
import '@babel/polyfill'

import Vue from 'vue'
```


#### 参考文章：

[ant-design-vue的兼容问题](https://blog.csdn.net/lydxwj/article/details/89912983)
