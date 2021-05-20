# 数据流以及持久化

## 框架

`redux` + `react-redux` + `redux-thunk` + `redux-persist`。

## 持久化

```javascript title="reducer/index.js"
const defaultState = {
  user: {
    id: 88888888,
    email: "i@cctv3.net",
    name: "SunYu peng",
  },
  users: [],
  reports: [],
  reportsPartial: [],
  setting: {
    time: {
      error: 30,
      anemia: 15,
      limit: 3, // 单位是分钟 -_-||
    },
    language: "en",
    device: {
      body: null,
      ecg: null,
      blood: null,
      fat: null,
    },
  },
  filter: {
    type: "",
    date: "",
    startTime: "2021-01-01",
    endTime: moment().format("YYYY-MM-DD"),
  },
  lastUploadTime: [],
  firstUse: {
    error: true,
    anemia: true,
    limit: true,
  },
  mode: "error",
  isSearching: false,
  searchHistory: [],
  adminConfig: {
    pageTypes: [],
    saveLines: {
      ecg: 100,
    },
  },
};
```
