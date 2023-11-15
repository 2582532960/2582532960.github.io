---
title: React分页功能实现
date: 2023-11-13 22:38:43
tags: [React, JavaScript]
categories: 前端
---

静态页面分页，定义 dataList 数组模拟后端返回数据

## 示例代码

```tsx
import React, { useState } from "react";
import styles from "./index.scss";
import { Pagination } from "antd";
import { RightOutlined } from "@ant-design/icons";
import { NavLink } from "react-router-dom";

export default function Trends() {
  const dataList = [
    {
      id: 1,
      title: "科技成果科技成果科技成果科技成果科技成果科技成果科技成果",
      time: "2023-11-13 12:21",
    },
    {
      id: 2,
      title: "科技成果科技成果科技成果科技成果科技成果科技成果科技成果",
      time: "2023-11-13 12:21",
    },
    {
      id: 3,
      title: "科技成果科技成果科技成果科技成果科技成果科技成果科技成果",
      time: "2023-11-13 12:21",
    },
    {
      id: 4,
      title: "科技成果科技成果科技成果科技成果科技成果科技成果科技成果",
      time: "2023-11-13 12:21",
    },
    {
      id: 5,
      title: "科技成果科技成果科技成果科技成果科技成果科技成果科技成果",
      time: "2023-11-13 12:21",
    },
    {
      id: 6,
      title:
        "科技成果科技成果科技成果科技成果科技成果科技成果科技成果科技成果科技成果科技成果科技成果科技成果科技成果科技成果",
      time: "2023-11-13 12:21",
    },
    {
      id: 7,
      title: "科技成果科技成果科技成果科技成果科技成果",
      time: "2023-11-13 12:21",
    },
    {
      id: 8,
      title: "科技成果科技成果科技成果科技成果科技成果科技成果科技成果",
      time: "2023-11-13 12:21",
    },
    {
      id: 9,
      title: "科技成果科技成果科技成果科技成果科技成果科技成果科技成果",
      time: "2023-11-13 12:21",
    },
    {
      id: 10,
      title: "科技成果科技成果科技成果科技成果科技成果科技成果科技成果",
      time: "2023-11-13 12:21",
    },
    {
      id: 11,
      title: "科技成果科技成果科技成果科技成果",
      time: "2023-11-13 12:21",
    },
    {
      id: 12,
      title: "科技成果科技成果科技成果科技成果科技成果科技成果科技成果",
      time: "2023-11-13 12:21",
    },
    {
      id: 13,
      title: "科技成果科技成果科技成果科技成果科技成果",
      time: "2023-11-13 12:21",
    },
  ];
  const [page, setPage] = useState(1); //当前页码
  const total = dataList.length;
  const [todosPerPage, setTodosPerPage] = useState(10); //存储每页上的项目数

  const lastTodoInView = page * todosPerPage;
  const firstTodoInView = lastTodoInView - todosPerPage;

  const todosForDisplay = dataList.slice(firstTodoInView, lastTodoInView);
  const handleChange = (pageNumber: any) => {
    setPage(pageNumber);
  };

  return (
    <div style={{ backgroundColor: "#f6f6f6" }}>
      <div className={styles.trends}>
        <NavLink to="/">首页</NavLink>
        <RightOutlined />
        <NavLink to="/science">科技成果</NavLink>
        <div className={styles.title}>科技成果</div>
        <div className={styles.trendsInner}>
          {todosForDisplay.map((item: any) => {
            return (
              <div key={item.id}>
                <NavLink
                  to={`/science/scienceDetail/${item.id}`}
                  className={styles.trends_item}
                >
                  <div className={styles.text}>{item.title}</div>
                  <div className={styles.time}>{item.time}</div>
                </NavLink>
              </div>
            );
          })}
        </div>
        <Pagination
          className={styles.pagination}
          defaultCurrent={1}
          current={page} //当前页码
          total={total} //总页数
          pageSize={todosPerPage} //存储每页上的项目数
          onChange={handleChange}
        />
      </div>
    </div>
  );
}
```

主要考验了对 slice 方法的掌握

## 定义和用法

slice() 方法可从已有的数组中返回选定的元素。

slice()方法可提取字符串的某个部分，并以新的字符串返回被提取的部分。

**注意：** slice() 方法不会改变原始数组。

## 语法

`array.slice(start, end)`

## 参数 Values

| 参数    | 描述                                                                                                                                                                                          |
| ------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _start_ | 可选。规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。                                                        |
| _end_   | 可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。 |

## 返回值

| Type  | 描述                                                                            |
| :---- | ------------------------------------------------------------------------------- |
| Array | 返回一个新的数组，包含从 start 到 end （不包括该元素）的 arrayObject 中的元素。 |

更多实例与解析见【菜鸟教程】
http://doc.yaojieyun.com/www.runoob.com/jsref/jsref-slice-array.html
