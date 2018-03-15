---
layout: post
title: 第三章程序基础知识
published: true
tags: [core_java]
---


源代码的文件名必须与公有类的名字一致，且以.java为后缀。必须注意大小写。

每个java程序都必须有一个main方法。

java的整形数据类型有四种：int，short，long，byte。
注意int没有c语言那样的有符号和无符号的区别。都是有符号的。
java整型的范围和运行的机器无关，也就是说无论是在32位机器和64位机器上，int型数据总是用4个字节存储的。 这一点和c语言不同。
int              4字节
short          2字节
long           8字节
byte           1字节
long型的数据后面必须带有“L”

java浮点型有两种：float，double。
float           4字节
double       8字节
一般默认使用double，双精度。因为单精度太小了，范围不够。

关键字 final 声明常量。习惯上，常量名使用大写。
类常量 经常希望一个常量在一个类中多个方法中使用。通常把这种常量称为类常量。
通常用static final 定义一个类常量。
类常量是在main方法外的。

Math类
Math.sqrt();
Math.pow();
Math.sin();
Math.round(); // 对小数四舍五入的运算
也可以不在方法前面添加类名，但是需要引入这个类。
import static java.lang.Math.*;
所以要想使用某个方法，有两种使用方法。
int  a = 4；  int b = Math.sqrt(a);
import static java.lang.Math.*;  int a = 4; int b = sqrt(a);
(注意，import后面必须添加 static。为什么还不知道）。因为调用的是静态方法啊。

懂了，上面的方法只限于静态方法，只有静态方法可以用
类名.方法（）          这个格式去调用静态方法。这个格式就表示调用静态方法了。


字符串
java没有字符串类型。所有字符串都是都是String类的一个实例。
String name = “Aimee";

字符串函数
s.substring();      得到字符串的一个子串
s.equals();         检测两个字符串相等。千万不能用 “==”检测是否相等；
s.length();          得到字符串长度;
s.charAt(n);      返回位置n的字符
int compareTo(String other)        按照字典顺序,比较字符串顺序
boolean endsWith(String suffix)    如果字符串以suffix结尾,范围true
boolean equals(Object other)
boolean equalsInnoreCase(String other) 忽略大小写比较
int indexOf(string str)
int indexOf(String str,int fromIndex)   


构建字符串
构建新的字符串可以使用StringBuilder类.
步骤: 首先构造一个空的字符串构造器
StringBuilder builder= new StringBuilder();
当每次需要添加一部分内容时,调用append方法
builder.append("a");
还有很多method可以再查询书


输入输出

读取输入
首先构造一个Scanner对象,并与标准输入流关联.
Scanner in= new scanner(System.in);
然后就可以使用scanner类的各种方法实现输入操作了
String name = in.nextLine();    //读取一行.可以包括空格
String name = in.next();       //读取一个单词
int age = in.nextInt();   //读取一个数
double = age2 = in.nextDouble();  //读取一个浮点数

注意,scanner类定义在java.util包里面.
当使用的类不是定义在java.lang包里面时,必须使用import将包引入

数组
java中的数组和c语言的数组格式上有些不一样.
c语言
int a[100];  //声明一个整型数组

java数组声明和初始化不一样
int[] a;    //声明一个整型数组.注意方括号位置不同
int[] a = new int[100];        //初始化这个整型数组
java中数组也是一个对象,所以也需要new一个数组.

简便的初始化数组的方式
int[] a = {1,3,4,6];   注意不需要new了
java有一个简单遍历数组的方式for each循环
```
for(int element : a){
     System.out.println(element);
}
```
数组拷贝
java允许将一个数组变量拷贝到令一个数组变量中,这其实是两个变量引用同一个数组.
int[] a = {1,2,3,4,5};
int[] b = a;
b[4] = 9;

这样a[4]也变成9了,而不是原来的5

如果想要把数组的值拷贝到另一个新的数组里面,就要使用Arrays类的copyOf方法
import java.util.Arrays;
public class Hello{
    public static void main(String[] args) { 
      int[]a = {1,3,4,5};
      int[]b = Arrays.copyOf(a,3);
      System.out.println(b[2]);
    }
}

copyOf()第二个参数是新数组的大小,这个方法通常用来增加数组的大小.
newString = Arrays.copyOf(oldString,oldString.length * 2);


数组初始化
1.int[] smallPrimes = {2,5,7};
2.使用匿名数组
new int[]{17,19,23};
使用这种方法可以在不创建新变量的情况下重新初始化一个数组。
smallPrimes = new int[]{17,19,23};


下面这个示例就是用了第二种方式
```
private static Image[] tankImags = null; // 存储全局静态
static {
        tankImags = new Image[] {
                tk.getImage(BombTank.class.getResource("Images/tankD.gif")), tk.getImage(BombTank.class.getResource("Images/tankU.gif")),
                tk.getImage(BombTank.class.getResource("Images/tankL.gif")),
                tk.getImage(BombTank.class.getResource("Images/tankR.gif")), };

}

```






























