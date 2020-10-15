# react-native第一天   
1. 第一个demo首先搭配环境              
   1. 环境搭配的时候走了很多弯路，相信网上的教程，网上教程多少有些久远，导致一直搭建不成功
   2. 最后公司负责人告诉我相信官网，我也没办法了，跟着官网一步一步的，结果很容易就成功了    
ps: 此处为我总结        
2. window 官网明确有node python2(此处必须2.几的) JDK Android-Studio      
   1. 官网说不能用cnpm但是我在家的时候用的就是cnpm也是没有问题的
   2. python2 的安装直接傻瓜式就行了，注意在 Customize Python这个页面的时候吧最后一项勾选为第一个will be installed on local hard drive这个，也就是第一项，这个意思就是给电脑自动配置环境。
   3. JDK安装，首先要根据操作系统下载对应的JDK，JDK下载版本不能太低，
   4. 傻瓜式安装，建议C盘，记下路径，安装完之后，去计算机->属性->高级系统设置->环境变量，新建系统变量"N": JAVA_HOME "V":刚才的路径，以我为例 C:\Program Files\Java\jdk1.8.0_181，在java中有多个文件夹，选择jdk路径，编辑系统变量Path，双击Path即可，新建变量值 %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin（电脑win10），新建系统变量"N": CLASSPATH "V": %JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar 之后在cmd窗口输入java 弹出内容为java相关的一大堆即安装成功。
   5. 安装Android Studio PS:http://www.android-studio.org/
   6. 安装Android Studio的时候每要记住勾选Android-SDK,Android-SDK-Platform, Performance (Intel  HAXM), Android-Virtual-Device,如果安装的时候有些是黑的不能勾选可以先跳过，
安装Android-SDK 这个需要注意官网了，因为RN版本与Android系统版本需要支持才行，有些Android版本RN并不支持。这个推荐看官网PS: https://reactnative.cn/docs/getting-started.html      