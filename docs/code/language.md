# 多语言配置

## 流程

### 获取系统语言

这里面有可能系统返回的中文的语言设置不一样，简体中文和繁体中文可能是 `zh-XXX`，所以最好先判断包含关系，然后匹配数组。

```javascript title="Main.js"
useEffect(() => {
  const askConfigs = () => {
  NativeModules.SystemModule.askConfig(s => {
    let result = JSON.parse(s);
    x.DEVICE.store.setIsTurnOn(result.isBluetoothTurnOn == 1);
    if (props.language == result.language) {
      // 没有设置语言
    } else {
      let ls = ['zh', 'en', 'de', 'it', 'fr', 'es', 'ja'];
      props.updateSettingLanguage(
        result.language.indexOf('zh') >= 0
          ? 'zh'
          : ls.some(it => it == result.language)
          ? result.language
          : 'en',
      );
    }
    x.DEVICE.store.setCountry(result.country);
  });
};
```

### 配置文件 ( 新版 )

之前旧版本是直接打包写死在本地的配置文件，新版本的是用 `JS 闭包` 写的单例模式，在 `Home` 页面加载完成之后，去服务器拉去对应的 `JSON` 文件，然后进行配置。

- 下载 `JSON` 文件

```javascript title="main.js"
useFocusEffect(
  useCallback(() => {
    // console.log('x.DEVICE.store.getLanguages()', JSON.stringify(x.DEVICE.store.getLanguages()));
    let file = RNFS.DocumentDirectoryPath + "/Test.json";
    let download = RNFS.downloadFile({
      fromUrl: "http://www.cctv3.net/Settings/Test.json",
      toFile: file,
      progress: (res) => {
        let percent =
          parseFloat((res.bytesWritten / res.contentLength) * 100).toFixed(2) +
          "%";
      },
    });
    download.promise.then((r) => {
      if (r.statusCode == 200) {
      }
    });
  }, [])
);
```

- 原生模块读取配置文件

```cpp title="SystemModule.java"
@ReactMethod
  public void file2Strings(String fileName, Callback callback) {
      File file = new File(getReactApplicationContext().getFilesDir(), fileName);
      HashMap<String, Object> hashMap = new HashMap<>();
      hashMap.put("status", 0);
      if(file.exists()) {
          hashMap.put("status", 1);
          try {
              List<String> list = FileUtils.readLines(file);
              StringBuilder sb = new StringBuilder();
              for(String s : list) {
                  sb.append(s);
              }
              hashMap.put("data", sb.toString());
          } catch (IOException e) {
              e.printStackTrace();
          }
      }
      callback.invoke(new Gson().toJson(hashMap));
  }
```

- 配置

```javascript title="main.js"
Platform.OS === "android" &&
  NativeModules.SystemModule.file2Strings("Test.json", (s) => {
    let result = JSON.parse(s);
    if (result.status == 1) {
      x.DEVICE.store.setLanguages(JSON.parse(result.data));
    }
  });
```

### 使用

```javascript
x.DEVICE.store.getLanguages().search[props.language];
```

### 配置文件 ( 旧版 → 废弃 )

`I18N.js` 里面配置了很多国家的语言，可以通过 `Java` 代码把 `Excel` 表转换成 `JSON`。

```cpp title="Main.java"
private void splitTranslateText() {
    try {
        String readLines = FileUtils.readFileToString(new File("ECGTranslater.txt"));
        String[] lines = readLines.split("\n");
        System.out.println(lines.length);
        String code[] = new String[] {"zh", "en", "de", "it", "fr", "es", "ja"};
        List<HashMap<String, Object>> list = new ArrayList<>();
        HashMap<String, Object> line = new HashMap<>();
        for(int i=0;i<lines.length;i++) {
            String s = lines[i];
            String[] ss = s.split("\t");
            if(ss.length == 7) {
                // System.out.println(s);
                HashMap<String, Object> hashMap = new HashMap<>();
                for(int j=0;j<7;j++) {
                    hashMap.put(code[j], ss[j]);
                }
                line.put(ss[0], hashMap);
            }
        }
        System.out.println(new Gson().toJson(line));
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

### 使用 ( 旧版 → 废弃 )

按照二维数组的方式去访问。

```javascript
I18ns.saveChanges[this.props.language];
I18ns[props.mode][props.language];
```
