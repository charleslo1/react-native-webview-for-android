# react-native-webview-for-android
> 为了修复 ReactNative 的 WebView 组件在安卓端不支持文件上传而包装的一个 Webview 组件，基于 [react-native-webview-file-upload](https://github.com/dongyaQin/react-native-webview-file-upload) 改造

<!-- MarkdownTOC -->

- [Installation](#installation)
  - [Manual Linking](#manual-linking)
  - [Automatic Linking](#automatic-linking)
- [Usage](#usage)
- [Contributing](#contributing)

<!-- /MarkdownTOC -->

## Install

```shell
npm install react-native-webview-for-android --save
```

### 自动 Linking
在项目目录下执行以下命令（如果失败，请使用手动 linking）
```shell
react-native link react-native-webview-for-android
```

### 手动 Linking

修改 `android/app/build.gradle` 文件：

```diff
 dependencies {
     //...
+    compile project(':react-native-webview-for-android')
 }
```

修改 `android/settings.gradle` 文件

```diff
 rootProject.name = 'YourAppName'

-include ':app'
+include ':app', ':react-native-webview-for-android'
+project(':react-native-webview-for-android').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-webview-for-android/android')
```


修改 `android/app/src/main/java/com/yourpackage/MainApplication.java` 文件

```diff
 //...
+import com.charleslo1.webview.AndroidWebViewPackage;

 //...

 public class MainApplication extends Application implements ReactApplication {
     //...
     @Override
     protected List<ReactPackage> getPackages() {
         return Arrays.<ReactPackage>asList(
             new MainReactPackage(),
+            new AndroidWebViewPackage()
         );
     }
     //...
 }
```

## Usage
在组件内引入 react-native-webview-for-android 组件，使用 Platform.select 根据平台渲染

```jsx
import React, { Component} from 'react';
import { WebView, View, Platform } from 'react-native';
// import AndroidWebView
import AndroidWebView from 'react-native-webview-for-android';

//...

class MyWebView extends Component {
  render() {
    return (
      <View style={{flex:1}}>
        {Platform.select({
          android: () => <AndroidWebView source={{ uri: 'https://www.baidu.com/' }}/>,
          ios: () => <WebView source={{ uri: 'https://www.baidu.com/' }}/>
        })()}
      </View>
    );
  }
}
```

