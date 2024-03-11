- [ ] 第三章 Activity
- [ ] ANKI 卡片一个单元
- [ ] 直击本质 书籍



[Day2_Note](Day2_Learn_Kotlin.md#kotlin魔法工具)

---
# Day3
## layout 
###  在页面中添加一个按钮
#### 加button的语法是
##### ```@+id/id_name```
#### android:layout_height 指定了当前元素的高度
- match_parent: 与父元素一样高
- wrap_content: 适应内容的高度
- 100dp: 100个像素的高度
#### android:text 指定了当前元素的文本内容
#### setContentView(R.layout.activity_main) 指定了当前页面的布局文件
> 项目中添加的任何资源文件都会在R文件中生成一个对应的id
> 所有的Activity都要在AndroidManifest.xml中注册
> 为程序配置一个启动的Activity

 #### 如何为程序配置一个启动的Activity
 - 在AndroidManifest.xml中的<activity>标签中内部加入<intent-filter>标签，然后在<intent-filter>标签中加入<action android:name="android.intent.action.MAIN"/>和<category android:name="android.intent.category.LAUNCHER"/>这两句声明

#### android:label 指定Activity中标题栏的内容
- 既是标题栏中的内容，也是启动器中的内容

### Toast
- What
  - Toast 是一种轻量级的提示，可以将一些短小的信息提示给用户，在过一段时间后自动消失，不会占用屏幕空间。
- How
  - 设置一个触发点
    ```kotlin
        val button: Button = findViewById(R.id.button)
        button.setOnClickListener {
            Toast.makeText(this, "You clicked me.", Toast.LENGTH_SHORT).show()
        }
    ```
- 静态方法
  - 什么是静态方法
    - 静态方法是指在类中定义的方法，可以直接通过类名调用，不需要实例化对象
- #### findViewById
  - 作用
    - 通过id找到对应的控件
  - 语法
    ```kotlin
        val button: Button = findViewById(R.id.button)
    ```
  - 说明
    - findViewById是Activity类中的一个方法，用于在布局文件中找到对应的控件
    - 尽量不使用findViewById，做法是直接调用自动生成的控件变量
  - 弊端 
    - 代码量大
    - 代码可读性差
    - 代码的可维护性差
### Menu
#### onCreateOptionsMenu
- 作用
- 
    ```kotlin
        override fun onCreateOptionsMenu(menu: Menu?): Boolean {
            menuInflater.inflate(R.menu.main, menu)
            return true
        }
    ```
