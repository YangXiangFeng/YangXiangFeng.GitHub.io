---
layout: post
title: 坦克大战中代码知识
published: true
tags: [java]
---
获取资源路径名

Url getResource(String name)
用法
类名.Class.getResource(String name);
比如我有一个文件叫做Test.java，可以通过这个方法获得想要的资源名。资源名字叫做image.gif,和Test.java在同一个文件里，那么就可以通过这个方法获得image.gif的路径。
```
public class PathTest {
    public static void main(String[] args) {
        System.out.println(PathTest.class.getResource("image.gif"));
    }
}
```



引入包容易出错.
子类对象也是超类的对象,引入包的时候不能只引入子类的包，还要引入超类的包。
案例分析
```
import java.util.ArrayList;
List<Tank> tanks = new ArrayList<Tank>();
```
这里只引入了ArrayList包，没引入List包，会导致出错。
修正：
```
import java.util.ArrayList;
import java.util.List;
List<Tank> tanks = new ArrayList<Tank>();
```
