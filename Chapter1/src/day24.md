# ***Day24 Java11新特性***

> Java9到Java11的新特性能用代码展示的倒是比较少

## 一、私有接口方法（Java9新增）

顾名思义，就是interface接口多了一个private方法

```java
package newFeature11;

import java.util.List;

@FunctionalInterface
public interface NewInterface {
    private void p() {
        System.out.println("123123");
    }

    default void l() {
        p();
    }

    void p123();
}

class RunMain {
    public static void main(String[] args) {
        NewInterface newInterface = () -> System.out.println("p123Method");
        newInterface.p123();
        newInterface.l();
    }
}
```

```
p123Method
123123

进程已结束，退出代码为 0
```

## 二、集合工厂方法

这个是集合多了一个of方法，但是这个方法创建的集合也就是List，Set和Map都是不可以更改的

```java
package newFeature11;

import java.util.List;

public class NewCollection {
    public static void main(String[] args) {
        List<Integer> list = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
        list.add(123);
    }
}
```

因为不可以更改但是我们做了更改所以会报错。

```
Exception in thread "main" java.lang.UnsupportedOperationException
	at java.base/java.util.ImmutableCollections.uoe(ImmutableCollections.java:71)
	at java.base/java.util.ImmutableCollections$AbstractImmutableCollection.add(ImmutableCollections.java:75)
	at newFeature11.NewCollection.main(NewCollection.java:8)

进程已结束，退出代码为 1
```

## 三、局部变量类型推断（var关键字 Java10新增）

这个也是顾名思义了，就是多了个var关键字，和JS和GO等等语言一样，多了这么一个自动获得类型的关键字，C++里其实也有这种关键字，只不过C++里面是auto

```java
package newFeature11;

import java.util.List;

public class NewCollection {
    public static void main(String[] args) {
        var list = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
        System.out.println(list);
    }
}
```

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

进程已结束，退出代码为 0
```

## 四、增强的 String API（Java11新增）

一些新的String的API

* isBlank() 判断是否为空白
* lines() 可以获得Stream类
* repeat(int) 重复次数
* strip() 和trim类似，去掉头尾的空格
* stripLeading() 去掉头部的空格
* stripTrailing() 去掉尾部的空格

```java
package newFeature11;

public class StringApiExample {
    public static void main(String[] args) {
        String text = "   Hello, World!   ";

        // isBlank() 是否为空白就要么空字符串要么全是空格
        System.out.println(text.isBlank()); // false

        // lines() 可以获得Stream类使用Stream的API
        text.lines().forEach(System.out::println);

        // repeat() 重复次数
        System.out.println("Hello".repeat(3)); // HelloHelloHello

        // strip() 去掉头尾的空格 不理解因为和trim一样的效果看上去
        System.out.println(text.strip()); // "Hello, World!"

        // stripLeading() and stripTrailing() 去掉开头的空格和结尾的空格
        System.out.println(text.stripLeading()); // "Hello, World!   "
        System.out.println(text.stripTrailing()); // "   Hello, World!"
    }
}
```

```
false
   Hello, World!   
HelloHelloHello
Hello, World!
Hello, World!   
   Hello, World!

进程已结束，退出代码为 0
```

## 五、标准 HTTP Client 升级

这下新增了HTTP的请求功能，可以直接发送请求了，不需要库就可以爬虫了，但是比起python确实还是麻烦了一些，但是调调API还是绰绰有余的。

```java
package newFeature11;

import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class HttpClientExample {
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(new URI("https://www.baidu.com"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println("Status code: " + response.statusCode());
        System.out.println("Body: " + response.body());
    }
}
```

```
Status code: 200
Body: <!DOCTYPE html>
<!--STATUS OK--><html> <head><meta http-equiv=content-type content=text/html;charset=utf-8><meta http-equiv=X-UA-Compatible content=IE=Edge><meta content=always name=referrer><link rel=stylesheet type=text/css href=https://ss1.bdstatic.com/5eN1bjq8AAUYm2zgoY3K/r/www/cache/bdorz/baidu.min.css><title>百度一下，你就知道</title></head> <body link=#0000cc> <div id=wrapper> <div id=head> <div class=head_wrapper> <div class=s_form> <div class=s_form_wrapper> <div id=lg> <img hidefocus=true src=//www.baidu.com/img/bd_logo1.png width=270 height=129> </div> <form id=form name=f action=//www.baidu.com/s class=fm> <input type=hidden name=bdorz_come value=1> <input type=hidden name=ie value=utf-8> <input type=hidden name=f value=8> <input type=hidden name=rsv_bp value=1> <input type=hidden name=rsv_idx value=1> <input type=hidden name=tn value=baidu><span class="bg s_ipt_wr"><input id=kw name=wd class=s_ipt value maxlength=255 autocomplete=off autofocus=autofocus></span><span class="bg s_btn_wr"><input type=submit id=su value=百度一下 class="bg s_btn" autofocus></span> </form> </div> </div> <div id=u1> <a href=http://news.baidu.com name=tj_trnews class=mnav>新闻</a> <a href=https://www.hao123.com name=tj_trhao123 class=mnav>hao123</a> <a href=http://map.baidu.com name=tj_trmap class=mnav>地图</a> <a href=http://v.baidu.com name=tj_trvideo class=mnav>视频</a> <a href=http://tieba.baidu.com name=tj_trtieba class=mnav>贴吧</a> <noscript> <a href=http://www.baidu.com/bdorz/login.gif?login&amp;tpl=mn&amp;u=http%3A%2F%2Fwww.baidu.com%2f%3fbdorz_come%3d1 name=tj_login class=lb>登录</a> </noscript> <script>document.write('<a href="http://www.baidu.com/bdorz/login.gif?login&tpl=mn&u='+ encodeURIComponent(window.location.href+ (window.location.search === "" ? "?" : "&")+ "bdorz_come=1")+ '" name="tj_login" class="lb">登录</a>');
                </script> <a href=//www.baidu.com/more/ name=tj_briicon class=bri style="display: block;">更多产品</a> </div> </div> </div> <div id=ftCon> <div id=ftConw> <p id=lh> <a href=http://home.baidu.com>关于百度</a> <a href=http://ir.baidu.com>About Baidu</a> </p> <p id=cp>&copy;2017&nbsp;Baidu&nbsp;<a href=http://www.baidu.com/duty/>使用百度前必读</a>&nbsp; <a href=http://jianyi.baidu.com/ class=cp-feedback>意见反馈</a>&nbsp;京ICP证030173号&nbsp; <img src=//www.baidu.com/img/gs.gif> </p> </div> </div> </div> </body> </html>


进程已结束，退出代码为 0
```

## 六、可以直接运行.java文件

> 这个我就不演示了，之前要javac之后才能java运行，现在可以直接对java文件使用java命令运行

### [上一章](day23.md)

### [下一章](day25.md)

### [返回目录](README.md)