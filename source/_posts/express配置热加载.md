---
title: express配置热加载
date: 2023-11-06 09:23:16
tags: [JavaScript, React, express]
categories: 前端
---

**前言**

本文基于 (“react”: “^16.13.1”) 版本

**1.参考 express 下的 package.json 文件**

express 的服务启动命令为：npm start

![](/images/express1.png)

**2.打开 react 项目的 package.json 文件，进行改写，增加 server 命令**

路径为 **express 项目名 /bin/www** ，须根据自己项目 express 服务文件夹名称进行改写

```json
"server": "node server/bin/www",
```

![](/images/express2.png)

**3.在 react 项目路径的基础上，启动 express 服务**

```javascript
npm run server
```

出现如下

![](/images/express3.png)

**4.express 实现自动刷新 (热加载)**

express 默认是没有热加载的，每次更改接口都需要重新启动，不然不生效

使用 nodemon 实现 express 热加载。

```javascript
npm  install nodemon --save
```

**5.改写 package.json （注意是 react 项目的 package.json）**

node 更改成 nodemon

```json
"server": "nodemon server/bin/www",
```

![](/images/express4.png)

**6.启动 npm run server**

```javascript
npm run server
```

至此配置热加载完成，以下为一条命令同时启动 react 项目以及 express 服务

**7.使用 concurrently (一条命令同时启动 react 项目以及 express 服务)**

```javascript
npm install concurrently --save
```

还是修改 react 项目的 package.json,增加 **dev** 命令

```json
"dev": "concurrently \"npm start\" \"npm run server\"",
```

![](/images/express5.png)

**8. 使用 dev 命令同时启动 react 项目以及 express 服务端**

```javascript
npm run dev
```

启动成功

![](/images/express6.png)

---

[点击查看原文](https://blog.csdn.net/weixin_43233914/article/details/105143620)
