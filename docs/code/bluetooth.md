# 硬件

## 流程

`Connect.js` 里面搜索设备，并且连接，连接成功以后跳转到 `Testing` 页面里面进行测量。

## 代码

## Devices.js

因为 `绑定设备` 页面和 `连接页面` 都是相同的逻辑，所以把搜索设备以及设备列表的展示逻辑封装成了组件 `<Devices />`，具体的使用方法可以参考上述两个页面。

## Testing (TestingMultiStep + TestSingleStep)

也就是测量页面，这里面的逻辑也最为复杂。修改这个逻辑的时候，为了保险起见，特意拉了一个新的分支 `Testing→SingleTest+MultiTest`。所以说有不明白的逻辑，可以拉一下这个分支。

### TestingMultiStep.js

测量模式二的页面。

### TestingSingleStep.js

测量模式一和三的页面。

## ECGDeviceModule.java

### `init(int timeout)`

```cpp
init(int timeout)
```

初始化 SDK 里面的实例。

### `ok()`

```cpp
ok()
```

配置完成，可以开始蓝牙设备的扫描。

### `checkPermission(CallBack callBack)`

```cpp
checkPermission(CallBack callBack)
```

`Android` 平台的蓝牙搜索设备需要开启精确定位权限。

### `disconnect(String mac)`

```cpp
disconnect(String mac)
```

断开指定 Mac 地址的设备。

### `clear(String mac)`

```cpp
clear(String mac)
```

清空指定 Mac 地址的设备的数据。

### `connect(String mac, boolean isClearData)`

```cpp
connect(String mac, boolean isClearData)
```

- **mac** → 将要连接的设备的 Mac 地址

- **isClear Data** → 是否清除设备上一次测量的数据

### `exportPdf(String pdfTitle, String id, String name, int age, String sex, String deviceName, Callback callback)`

```cpp
exportPdf(String pdfTitle, String id, String name, int age, String sex, String deviceName, Callback callback)
```

生成测量报告的 Pdf。
