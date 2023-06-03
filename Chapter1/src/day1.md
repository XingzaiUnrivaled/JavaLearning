# ***Day1 第一个Java程序***

## 第一章 认识Java

> 其实看百度百科就差不多了解了点一下这个链接就行了[Java百科](https://www.baidu.com)  
> 简单概括一下其实就是一个叫做 詹姆斯·高斯林 的人在C++的基础上创建了 Java 并且是有着想让 Java 跨平台的想法的，所以就在Sun公司里面开发了
> Java 这门语言，火了是后话。后面 Sun 也因为 Java 的原因被甲骨文 Oracle 看上了就被收购了

简单介绍一下Java的结构，首先是对Java的理解，我当初是因为MC所以接触的Java，其实Java分很多种类型，有三种，分别为: jdk jre jvm

* java的程序是在jvm (java virtual machine/Java虚拟机)上运行的
* jre (java runtime environment/Java运行环境) 包含jvm和java要运行一些工具
* jdk (java development kit/Java开发工具) 包含jre和java开发的一些工具

所以其实如果只是玩mc下载jre就足够了，当然下载jdk也是一样，因为jdk包含了jre，这就是三者的关系，然后一般市面上只有jdk和jre可以下载。jvm都是雪藏的

### [Java的下载(甲骨文官网)](https://www.oracle.com)

点进这个链接其实就可以找到Java了，在最上面一览找到 Products (产品) 下拉菜单里面有 [Java](https://www.oracle.com/java/)
，也可以直接点击我这个链接快速到达，然后在右边有个 Download Java (下载Java)
，点击我这个链接也可以快速到达[点我速达下载页面](https://www.oracle.com/java/technologies/downloads/)  
然后往下翻，直接把Java8，Java11和Java17全部下载了。无所谓只要继续学Java以后肯定会有用的😁

# 第二章 配置环境变量

1. 首先对着 `此电脑` 按右键 (因为基础也只在windows上搞过，在Mac上也都是直接使用idea了😋) 点击 `属性(R)`
   ，如果你桌面上没有此电脑那你可以去百度一下怎么弄出来或者按
   `Win + E` 呼出资源管理器，对左边的 `此电脑` 按右键点 `属性`
2. 然后在右边或者下面找到`高级系统设置`，当然如果你不想执行第一步也可以使用`Win + I`呼出设置菜单，在左边搜索高级系统设置
3. 然后点击`环境变量(N)`，再点击`系统变量`下方的新建，在 `变量名(N)` 里面填写 `JAVA_HOME` 然后在 `变量值(V)`
   里面路径，看你想配置哪个版本的Java就填哪个版本的路径，默认都在C盘如果你是自己换了其他盘的路径自己换就完事了，填到该Java为止，默认都在`
   C:\Program Files\Java`，举个栗子: 假如我要配置Java8的环境变量，然后我安装的Java8是默认安装的，然后我的Java8的版本是333，所以我在
   **变量值(V)** 填写的就是 `C:\Program Files\Java\jdk1.8.0_333` (引号不要)
4. 如果填写完确定好之后，你的系统变量里就多出了一个JAVA_HOME的变量，双击点开Path的这个变量 (
   强调是系统变量里的，因为刚刚配置的`JAVA_HOME`也是在系统变量里的)，然后点击右边的新建然后填入 `JAVA_HOME\bin`，最后把这个
   JAVA_HOME\bin 按上移移动到最上面，配置结束
5. 全部点击确定出来，然后我们来验证了，按Win键搜索cmd敲回车，输入命令 javac
   如果弹出一大串说明是配置好了,如果弹出的是 `'javac' 不是内部或外部命令，也不是可运行的程序
   或批处理文件。`那说明你配置失败啦，重复上面四步  
   欧克，你现在配置完环境变量啦，你可以使用命令行进行编译啦。

# 第三章 第一个程序 打印Hello World

> 经过前面两步，你已经配置完环境变量了，可以正常的写代码进行编译了。

首先先创建一个文本文件 (没有后缀.txt的上网百度一下，怎么打开查看文件后缀)，将它命名为`Hello.java`
然后我们右键点击编辑开始编辑，写入

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello world");
    }
}
```

然后保存并关闭，在这个创建了该文件的文件夹下打开cmd，并输入`javac Hello.java`
并回车，你会发现没有任何的报错和响应，说明成功了，注意：文件名是`Hello.java`
然后代码里的`class后面的名字也应该是Hello和文件名相同`，正常情况就编译成功了，然后这个文件夹下就出现了`Hello.class`
，如果没有刷新一下，如果刷新了还没有然后使用`javac`编译也没有报错说明肯定有了的，仔细看看。  
然后在命令行也就是cmd中继续使用`java Hello`注意这次不能带上后缀，他会在命令行打印`Hello world`，这就是你的第一个程序
