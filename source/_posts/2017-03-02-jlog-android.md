---
title: jlog  Android日志
date: 2017-03-02 17:23:24
tags:
categories: 技术分享
---

最近需要在项目中加入将日志存储到文件的功能，本着“不要重复造轮子的原则”，施展 “Google+GitHub” 大法，找到了这个项目 —— [jlog](https://github.com/JiongBull/jlog/blob/master/README_ZH.md)。

### 添加依赖

在根目录的build.gradle里添加仓库。
```
allprojects {
 repositories {
    jcenter()
    maven { url "https://jitpack.io" }
 }
 ```
在模块的build.gradle中添加依赖。
```
dependencies {
     compile 'com.github.JiongBull:jlog:0.1.0'
}
```

### 初始化

建议在你的 application 的 onCreate() 方法里初始化 jlog 的全局配置，设置一次终身受用。

```java
public class RootApp extends Application {
    private static Logger sLogger;

    @Override
    public void onCreate() {
        super.onCreate();
        List<String> logLevels = new ArrayList<>();
        logLevels.add(LogLevel.ERROR);
        logLevels.add(LogLevel.WTF);

        sLogger = Logger.Builder.newBuilder(getApplicationContext(), "jlog")
                .setDebug(true) //是否开启调试模式
                .setWriteToFile(true) //是否输出日志到文件
                .setLogDir(getString(R.string.app_name))
                .setLogPrefix("")
                .setLogSegment(LogSegment.TWELVE_HOURS)
                .setLogLevelsForFile(logLevels)
                .setZoneOffset(TimeUtils.ZoneOffset.P0800)
                .setTimeFormat("yyyy-MM-dd HH:mm:ss")
                .setPackagedLevel(1)
                .setStorage(null)
                .build();
    }

    public static Logger getsLogger() {
        return sLogger;
    }
}
```
### 注意事项
要写文件到sd卡中，在 AndroidManifest 添加权限
```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```
还有，如果是把 Logger 的初始化写到 application 中，一定不要忘记在 application标签中添加 name 属性。
```xml
<application
        android:name=".RootApp"
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
```
### 使用
使用非常简单，如下
```java
    RootApp.getsLogger().e("log","hello logeer");
    RootApp.getsLogger().d("log","hello logger");
```
这样，在 logcat 和内部 sd 卡中，都可以看到输出的日志
更多详细的配置请参见 GitHub 上的文档。
