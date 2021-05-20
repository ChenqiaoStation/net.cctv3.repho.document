# 多语言配置

## 流程

### 获取系统语言

``` javascript title="Hello.js"
useEffect(() => {
  appStater = AppState.addEventListener("change", (thisState) => {
    console.log("App state", thisState);
    NativeModules.SystemModule.askConfig((s) => {
      let result = JSON.parse(s);
      x.DEVICE.store.setIsTurnOn(result.isBluetoothTurnOn == 1);
      if (props.language == result.language) {
        // 没有设置语言
      } else {
        let ls = ["zh", "en", "de", "it", "fr", "es", "ja"];
        props.updateSettingLanguage(
          ls.some((it) => it == result.language) ? result.language : "en"
        );
      }
      x.DEVICE.store.setCountry(result.country);
    });
  });
}, []);
```

### 配置文件

`I18N.js` 里面配置了很多国家的语言，可以通过 `Java` 代码把 `Excel` 表转换成 `JSON`。

``` cpp title="Main.java"
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

### 使用

按照二维数组的方式去访问。

```javascript
I18ns.saveChanges[this.props.language];
I18ns[props.mode][props.language];
```
