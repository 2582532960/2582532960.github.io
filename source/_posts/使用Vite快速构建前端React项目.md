---
title: 使用 Vite 快速构建前端 React 项目
date: 2023-11-06 12:48:01
tags: [React, Vite]
categories: 前端
---

## 一、初始化项目

首先，在终端命令行中输入如下的命令：

```javascript
npm create vite
```

```json
✔ Project name: vite-project
? Select a framework: › - Use arrow-keys. Return to submit.
    vanilla // 无前端框架
    vue     // 基于 Vue
 >  react   // 基于 React
    preact  // 基于 Preact（一款精简版的类 React 框架）
    lit     // 基于 lit（一款 Web Components 框架）
    svelte  // 基于 Svelte
```

此处，我们选择构建的框架为 React。接着，执行如下命令在启动本地项目：

```javascript
cd vite-project
npm install
npm run dev
```

安装完成之后，去浏览器中打开 localhost://5173/页面就可以看到示例项目了。

## 二、配置文件

路径别名的配置（vite.config.ts）

```javascript
// vite.config.ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
// 引入 path 包注意两点:
// 1. 为避免类型报错，你需要通过 `pnpm i @types/node -D` 安装类型
// 2. tsconfig.node.json 中设置 `allowSyntheticDefaultImports: true`，以允许下面的 default 导入方式
import path from "path";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
});
```

配置路径别名的提示（tsconfig.json）

```javascript
// tsconfig.json
{
  "compilerOptions": {
    ...
    "baseUrl": "./",
    "paths": {
      "@/*": ["./src/*"],
    }
  }
}
```

## 三、集成 react-router

```javascript
npm i --save-dev react-router-dom //这里可以使用cnpm代替npm命令

//说明： -save-dev 的意思是将模块安装到项目目录下，并在package文件的devDependencies节点写入依赖。

//总结--save-dev和-save的区别如下:
//devDependencies 节点下的模块是我们在开发时需要用的，比如项目中使用的 gulp ，压缩css、js的模块。这些模块在我们的项目部署后是不需要的，所以我们可以使用 -save-dev 的形式安装。像 express 这些模块是项目运行必备的，应该安装在 dependencies 节点下，所以我们应该使用 -save 的形式安装。
```

[路由官网](https://reactrouter.com/en/main/start/overview)

[中文文档](http://www.reactrouter.cn/docs/api#routes-%E5%92%8C-route)

## 四、集成 Antd

```javascript
npm install antd --save
```

图标

```javascript
npm install @ant-design/icons --save
```

## 五、样式

reset.css 是一种 CSS 文件，它的作用是重置网页的默认样式。由于不同浏览器对于 HTML 默认样式的设定不同，导致网页在不同浏览器上的显示效果各异。为了避免这种情况，可以使用 reset.css 对网页默认样式进行重置，使不同浏览器上的显示效果尽量一致。

现在需要对全部的样式进行清除，使用命令导入依赖：

```javascript
npm i reset-css
```

然后在 main.tsx 中进行引入，引入的位置必须要在`import App from "./App.tsx";`上面

```javascript
import "reset-css";
```

安装 sass

```javascript
npm i --save-dev sass
```
