# 数据流以及持久化

## 框架

`redux` + `react-redux` + `redux-thunk` + `redux-persist`。

## 持久化

```javascript title="reducer/index.js"
const defaultState = {
  user: {
    // 登录的用户的信息
    id: 88888888,
    email: "i@cctv3.net",
    name: "SunYu peng", 
  },
  users: [], // 登录用户下面的所有的测量用户
  reports: [], // 所有的测量报告
  reportsPartial: [], // 测量报告的过滤部分 → 不管是搜索的还是过滤的报告
  setting: {
    // 关于 APP 的设置信息
    time: {
      // 测量时间的设置
      error: 30, // 心律失常 单位 / 秒
      anemia: 15, // 心肌缺血 单位 / 秒
      limit: 3, // 心脏负荷 单位 / 分钟
    },
    language: "en", // 多语言设置
    device: {
      // 绑定设备
      body: null,
      ecg: null,
      blood: null,
      fat: null,
    },
  },
  filter: {
    // 报告页面过滤的条件
    type: "",
    date: "",
    startTime: "2021-01-01",
    endTime: moment().format("YYYY-MM-DD"),
  },
  lastUploadTime: [], // ECG 首页会有一个最后测量时间的展示
  firstUse: {
    // 各个模式是不是首次使用，首次使用加载默认的轮播图，一旦测量过程结束，第二次以及后都加载网络图片
    error: true, // 心律失常
    anemia: true, // 心肌缺血
    limit: true, // 心脏负荷
  },
  mode: "error", // 当前的测量模式
  isSearching: false, // 是否正在搜索
  searchHistory: [], // 搜索历史的关键词
  adminConfig: {
    // 暂未使用
    pageTypes: [],
    saveLines: {
      ecg: 100,
    },
  },
};
```
