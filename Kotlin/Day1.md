# Kotlin

## Day 1
### Get Used to Android Studio
#### Structure of a android project
- .gradle
  - It generated automatically by Android Studio
- .idea
  - It generated automatically by Android Studio
- app
  - build
    - 在编译时自动生成的文件
  - gradle
    - gradle wrapper: 
  - app 只有app目录下的文件才是我们的工作重点
  - libs
    - 一些第三方库
  - androidTest
    - 可以写一些自动化测试
  - java
    - 包含了我们的代码
    - 以及kotlin代码
  - res
    - 包含了我们的资源文件
    - layout
      - 布局文件
    - mipmap
      - 图标文件
    - values
      - 颜色、字符串等资源文件
    - drawable
      - 图片资源文件
  - AndroidManifest.xml
    - Android的配置文件
    - 四大组建：Activity、Service、BroadcastReceiver、ContentProvider
```
        在这里注册activity
        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:label="@string/app_name"
            android:theme="@style/Theme.Helloworld">
            <intent-filter> 非常重要
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
                这个表示这个activity是启动的入口
            </intent-filter>
        </activity>
```

- Activity是安卓应用程序的门面。凡是用户可以看到的界面，都是Activity。

### MainActivity
- AppCompatActivity
  - 是Activity的子类
  - 为了兼容低版本的Android系统
  - 一般情况下，我们的Activity都应该继承自AppCompatActivity
- onCreate
  - Activity的生命周期方法
  - 在Activity第一次创建的时候调用
  - 一般用来初始化界面
> 安卓的程序设计讲究逻辑和视图分离。逻辑写在Activity中，视图写在xml文件中。
### 如何引用一个应用程序名称
- @string/app_name 在XML中引用
  - @string表示引用一个字符串资源
  - app_name是字符串资源的名字
  - 在res/values/strings.xml中定义了app_name
- R.string.app_name 在Java中引用
  - R是一个类
  - string是一个内部类
  - app_name是一个静态常量
  - R.string.app_name就是一个int类型的常量
  - 通过这个int类型的常量，我们可以找到strings.xml中的app_name
- string可以替换成drawable、color等
- 通过R类，我们可以找到res目录下的所有资源文件

### 详解build.gradle
- Gradle是一个项目构建工具
- 使用了Groovy语言（DSL）来进行项目设置。


### 日志工具
- Log.v() 用于打印最为琐碎的，意义最小的日志
- Log.d() 用于打印调试日志，对应级别debug，比verbose高一级。
- Log.i() 用于打印一些重要数据，可以帮助分析用户行为，对应级别info，比debug高一级。
- Log.w() 用于打印一些警告信息，对应级别warn，比info高一级。
- Log.e() 用于打印错误信息，对应级别error，比warn高一级。
- 当然信息也需要过滤。

### 为什么使用Log而不是println（）
- println（）缺点
  - 日至开关不可控制 不能添加日至标签，日志没有级别区分
  - Log级别从低到高：verbose、debug、info、warn、error
- Logcat功能
  - 添加过滤器