# 导航

## 版本

- **0.59.10** → react-navigation `3.x`。

- **0.64.3** → react-navigation `5.x`。

## 配置

配置入口 `App.js`。

```javascript title="页面结构"
├── Account // Tab3 用户中心
│   ├── Guide.js // 用户使用手册
│   ├── MyDevice.js // 设备绑定
│   ├── PdfViewer.js // Pdf 文件预览 → 测量报告的生成页
│   ├── TestSetting.js // 设置测量时间
│   └── index.js
├── Button.js // 自定义组件 渐变色的按钮
├── DeviceFactory.js // 屏幕适配的工具类
├── Drapdown.js // 自定义组件 → 下拉选择框
├── ECG // Tab 1 ECG 首页
│   ├── Connect.js // 设备连接
│   ├── Device.js // 自定义组件 → 设备列表的一个 ITEM
│   ├── Devices.js // 自定义组件 → 设备列表 → 可以看作是上面的 Device Item 的一个集合
│   ├── How2Use.js // 模式二测量过程中的轮播图
│   ├── TestingItems.js // 自定义组件 → 从左到右依次是 心率 倒计时 和 电量
│   ├── TestingMultiStep.js // 模式二测量页面
│   ├── TestingSingleStep4Android.js // 模式一和模式三测量页面 → Android 平台
│   ├── TestingSingleStep4iOS.js // 模式一和模式三测量页面 → iOS 平台
│   └── index.js
├── ECGViewer.js // 自定义组件 → 原生的心电图的 View
├── Reports // Tab2 报告页
│   ├── Filter.js // 根据条件过滤的过滤页
│   ├── List.js // 自定义组件报告列表 → 不管是搜索还是过滤页面都是这一个列表
│   ├── Search.js // 搜索页面 → 可以看作是 SearchHistory 和 SearchResult 的合集
│   ├── SearchHistory.js // 自定义组件 → 搜索历史
│   ├── SearchResult.js // 自定义组件 → 搜索结果
│   └── index.js
├── SearchView.js // 自定义组件 → 搜索框
├── Switcher.js // 自定义组件 → 单选开关
├── TabBar.js // 自定义组件 → 顶部的 Tab
├── Toast.js // 自定义组件 → 吐司
├── UCWeb.js // 自定义组件 → WebView
├── User // 用户相关
│   ├── ChooseUser.js // 选择测量用户列表
│   ├── EditUser.js // 编辑测量用户的详细信息
│   ├── ManageUser.js // 编辑测量用户列表
│   ├── NewUser.js // 新建测量用户
│   └── UserForm.js // 编辑或者新增测量用户的表单
├── WaitView.js // 自定义组件 → 等待效果的 View
└── iPhoneX.js // iPhone X 适配
```
