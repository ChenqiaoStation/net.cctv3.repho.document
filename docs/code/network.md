# 网络请求

## 框架

- 普通的表单的提交 → fetch
- 文件下载 → RNFS

## 配置

### x.js

1. 提供了几种环境，打包的时候注意切换至指定的环境。

```javascript
// dev alpha bate production
x.DEVICE.ENVIRONMENT = dev;
```

2. x.API.xxx
   构件表单直接在这里面添加即可。

- to: 哪个接口。

- data: 生成对应的 `JSON` 对象。

### Server.js

1. 配置不同环境的服务器的主机。
2. 封装了常用的 `GET` `POST` `UPLOAD` 等方法。

```javascript title="Service.js"
this.services = {
  // 开发环境
  // http://192.168.9.252:7002/cloud
  // http://192.168.9.12:7001
  dev: "http://192.168.9.252:7001",
  // 内部测试环境
  alpha: "",
  // 预发布环境
  bate: "",
  // 生产环境
  // http://renpho-cloud-73575627.us-east-1.elb.amazonaws.com/cloud
  // https://cloud.renpho.com
  production: "http://renpho-cloud-73575627.us-east-1.elb.amazonaws.com/cloud",
};
```

## 使用

完整的使用流程。

```javascript
export const downloadUsers = (userId) => {
  let service = new Service();
  return (dispatch) => {
    service
      .asyncPost(
        service.getService() + x.API.queryUserList.to,
        JSON.stringify(x.API.queryUserList.data(userId))
      )
      .then((json) => {
        dispatch({
          type: DOWNLOAD_USERS,
          value: x.ARRAY.sortUsersByMainUser(json.result.list),
        });
      });
  };
};
```
