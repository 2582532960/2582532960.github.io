---
title: Reat父子组件的通信
date: 2023-11-06 14:51:40
tags: React
categories: 前端
---

## 一、父组件向子组件传值（props）

父组件：

```javascript
import Son from "@/Test/Son";

export default function Father() {
  return (
    <div>
      我是父组件
      <hr />
      <Son name="小明" age="18" />
    </div>
  );
}
```

子组件:

```javascript
export default function Son(props: any) {
  return (
    <div>
      我是子组件 我是{props.name},我的年龄是{props.age}
    </div>
  );
}
```

浏览器运行效果：
![](/images/communication1.png)

## 二、子组件向父组件传值：通过自定义方法的方式

父组件：

```javascript
import Son from "@/Test/Son";

export default function Father() {
  const fatherFun = (value: any) => {
    alert(value);
  };
  return (
    <div>
      我是父组件
      <hr />
      <Son name="小明" age="18" sonValue={fatherFun} />
    </div>
  );
}
```

子组件：

```javascript
export default function Son(props: any) {
  const toFather = (value: any) => {
    props.sonValue(value);
  };
  return (
    <div>
      我是子组件 我是{props.name},我的年龄是{props.age}
      <button
        onClick={() => {
          toFather("我是子组件传过来的数据");
        }}
      >
        点我向父组件传数据
      </button>
    </div>
  );
}
```

浏览器运行效果：
![](/images/communication2.png)

## 三、state：状态管理：可以更新页面里面的数据的状态，使页面重新渲染。

**演示一**

父组件：

```javascript
import Son from "@/Test/Son";
import { useState } from "react";

export default function Father() {
  const [weather, setWeather] = useState(true);
  return (
    <div>
      我是父组件
      <hr />
      今天的天气很{weather ? "晴朗" : "阴暗"}
      <Son
        weather={weather}
        changeWeather={() => {
          setWeather(!weather);
        }}
      />
    </div>
  );
}
```

子组件：

```javascript
export default function Son2(props: any) {
  const handleChangeWeather = (value: any) => {
    props.changeWeather(value);
  };
  return (
    <div>
      <button
        onClick={() => {
          handleChangeWeather("");
        }}
      >
        改变天气
      </button>
    </div>
  );
}
```

**演示二**

父组件：

```javascript
import Son from "@/Test/Son";
import { useState } from "react";

export default function Father() {
  const [name, setName] = useState("小明");
  return (
    <div>
      我是父组件
      <hr />
      我点击的是{name}
      <Son
        showName={(value: any) => {
          setName(value);
        }}
      />
    </div>
  );
}
```

子组件：

```javascript
export default function Son2(props: any) {
  const data = [
    {
      id: 1,
      name: "小明",
    },
    {
      id: 2,
      name: "小兰",
    },
    {
      id: 3,
      name: "小红",
    },
  ];
  const handleShow = (value: any) => {
    props.showName(value);
  };
  return (
    <div>
      {data.map((item: any) => {
        return (
          <button
            key={item.id}
            onClick={() => {
              handleShow(item.name);
            }}
          >
            {item.name}
          </button>
        );
      })}
    </div>
  );
}
```

浏览器运行效果：
![](/images/communication3.png)
