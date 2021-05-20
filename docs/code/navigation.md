# 导航

## 版本

- **0.59.10** → react-navigation `3.x`。

- **0.64.3** → react-navigation `5.x`。

## 配置

配置入口 `App.js`。

```javascript title="App.js"
import * as React from "react";
import { Button, View } from "react-native";
import { NavigationContainer } from "@react-navigation/native";
import {
  CardStyleInterpolators,
  createStackNavigator,
} from "@react-navigation/stack";
import Main from "./main";
import ECG from "./pages/ECG";
import ChooseUser from "./pages/User/ChooseUser";
import EditUser from "./pages/User/EditUser";
import NewUser from "./pages/User/NewUser";
import How2Use from "./pages/ECG/How2Use";
import Search from "./pages/Reports/Search";
import ManageUser from "./pages/User/ManageUser";
import TestSetting from "./pages/Account/TestSetting";
import MyDevice from "./pages/Account/MyDevice";
import PdfViewer from "./pages/Account/PdfViewer";
import Guide from "./pages/Account/Guide";
import UCWeb from "./pages/UCWeb";
import Filter from "./pages/Reports/Filter";
import Connect from "./pages/ECG/Connect";
import TestingMultiStep from "./pages/ECG/TestingMultiStep";
import TestingSingleStep from "./pages/ECG/TestingSingleStep";

import Home from "./pages/Home";

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator
        headerMode="none"
        mode="card"
        screenOptions={{
          cardStyleInterpolator: CardStyleInterpolators.forHorizontalIOS,
        }}
      >
        <Stack.Screen name="Home" component={Home} />
        <Stack.Screen name="Main" component={Main} />
        <Stack.Screen name="ChooseUser" component={ChooseUser} />
        <Stack.Screen name="Connect" component={Connect} />
        <Stack.Screen name="TestingMultiStep" component={TestingMultiStep} />
        <Stack.Screen name="TestingSingleStep" component={TestingSingleStep} />
        <Stack.Screen name="Filter" component={Filter} />
        <Stack.Screen name="PdfViewer" component={PdfViewer} />
        <Stack.Screen name="How2Use" component={How2Use} />
        <Stack.Screen name="EditUser" component={EditUser} />
        <Stack.Screen name="NewUser" component={NewUser} />
        <Stack.Screen name="ECG" component={ECG} />
        <Stack.Screen name="Search" component={Search} />
        <Stack.Screen name="ManageUser" component={ManageUser} />
        <Stack.Screen name="TestSetting" component={TestSetting} />
        <Stack.Screen name="MyDevice" component={MyDevice} />
        <Stack.Screen name="Guide" component={Guide} />
        <Stack.Screen name="UCWeb" component={UCWeb} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```
