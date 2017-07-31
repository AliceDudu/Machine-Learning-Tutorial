#### 1. 安装 sbt

打开 terminal，检查 java 版本，安装 sbt：
http://www.scala-sbt.org/release/docs/Installing-sbt-on-Mac.html

```
$ java -version

$ brew install sbt

$ sbt about
Getting org.scala-sbt sbt 0.13.16
```

---

#### 2. 下载 jetbrains 的 community 版本, 安装 Scala plugin
打开 dmg 文件安装：
https://www.jetbrains.com/idea/download/#section=mac

点击左下角：skip all
![](http://upload-images.jianshu.io/upload_images/1667471-c9ebbb6d84e5e197.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在 configure 下拉选择 plugins：
![](http://upload-images.jianshu.io/upload_images/1667471-147587a246185c21.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

左下角选择 install jetbrains plugin：
![](http://upload-images.jianshu.io/upload_images/1667471-fa11b36c22bc80e3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

搜索框搜 scala，点击 install，安装后这个绿色键会变成 restart，点击：
![](http://upload-images.jianshu.io/upload_images/1667471-a1485b07437996b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

选择 restart：
![](http://upload-images.jianshu.io/upload_images/1667471-268f564f5cf3ea69.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

#### 3. 创建 scala project

选择 create new project：
![](http://upload-images.jianshu.io/upload_images/1667471-1c1359ce3a08a791.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


选择 scala － sbt：
![](http://upload-images.jianshu.io/upload_images/1667471-23ca4d5b677ae9e4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

为项目命名，确认 JDK 为配置的版本：
![](http://upload-images.jianshu.io/upload_images/1667471-ae110edb44e46a15.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

#### 4. 创建 scala worksheet

在项目下，如图所示创建 scala worksheet：
![](http://upload-images.jianshu.io/upload_images/1667471-a9672ce30a19c5ce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以输入 hello world ：
![](http://upload-images.jianshu.io/upload_images/1667471-7d657eb0127052bc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

#### 5. 创建 scala class

新建 scala class 的方法：
![](http://upload-images.jianshu.io/upload_images/1667471-a4cc9ed00fbb1025.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

命名：
![](http://upload-images.jianshu.io/upload_images/1667471-d922c2cedb65ba2d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在新建的 class 里面写上下面的代码：
```
package ex

object example extends App {
  println("Hello World")
}
```

运行，可以看到输出结果：
![](http://upload-images.jianshu.io/upload_images/1667471-ac025395e912a9a0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

#### 6. 打开 SBT project 的方法

在 Intelli J 的导航 file 处先关闭当前项目：

![](http://upload-images.jianshu.io/upload_images/1667471-adcdf61f31909d4c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

选择 import：
![](http://upload-images.jianshu.io/upload_images/1667471-cfefbe2f95307521.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


选择 build.sbt：
![](http://upload-images.jianshu.io/upload_images/1667471-6ad17211af3a273a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



![](http://upload-images.jianshu.io/upload_images/1667471-6966fda3a11f1a97.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![](http://upload-images.jianshu.io/upload_images/1667471-6f5e999a443aec17.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

#### 7. 同步 SBT and IntelliJ IDEA projects

IntelliJ IDEA SBT 支持项目同步，当 scala 版本更新或者增加 library 时，项目可以自动更新。

打开 build 文件：

当前 scalavesion 版本是 2.12，将相应代码加进去：

```
libraryDependencies += "org.scalatest" %% "scalatest" % "3.0.0" % "test"
```
其它版本可以查看：http://www.scalatest.org/older_releases

![](http://upload-images.jianshu.io/upload_images/1667471-c2ae609cb50e904a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![](http://upload-images.jianshu.io/upload_images/1667471-ea6b8f8c930d9f32.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

#### 8. 可以用 terminal  执行 sbt 命令

打开 intellij 左下角的 Terminal：

输入
```
$ sbt

>compile
```

![](http://upload-images.jianshu.io/upload_images/1667471-74ad32de8a320a19.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---
推荐阅读
[历史技术博文链接汇总](http://blog.csdn.net/aliceyangxi1987/article/details/71911003)
也许可以找到你想要的：
[入门问题][TensorFlow][深度学习][强化学习][神经网络][机器学习][自然语言处理][聊天机器人]

---

公众号 机器学习X计划 同步更新，欢迎扫码关注！

![机器学习X计划](http://upload-images.jianshu.io/upload_images/1667471-4bb4f955eaf6087e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
