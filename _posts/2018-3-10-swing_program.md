# 框架
 什么是框架呢？就是顶层窗口（没有包含在其他窗口中的窗口）。
 首先定义一个关闭这个框架时的响应动作。这里这个动作就是退出.
 在包含多个框架的程序中不能关闭一个框架就让程序退出，
 >在默认情况下只是将程序隐藏起来而不是退出

``` 
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
```
简单的构造框架程序是不会自动显示出来的，框架起初是不可见的。这样就可以在框架显示之前
往其中添加组件。
frame.setVisible(true);

awt和Swing框架的继承层次.它们都是类
Object->Component->Container->Window->Frame->JFrame

Swing框架是基于awt框架开发出来的，但是并没有代替awt框架，它仅仅是提供了更加强大的组件.
在awt库中,有一个称为Frame的类,用于描述顶层窗口.这个类的Swing版本名为JFame,它扩展于Frame类.
绝大多数Swing组件都有 "J"开头

Object->Component->Container->JComponent->JPanel

框架定位
JFrame框架本身用于改变窗口外观的方法很少，但是它的超类里有很多方法。
java.awt.Component类
setLocation(x,y)   设置框架在屏幕的位置，
setBounds(x,y,width,height)  设置位置和长和宽
setIconImage()告诉窗口系统在标题栏，任务切换窗口等位置显示哪个图标
setTitle()  设置标题栏标题
setResizable() 决定框架大小是否可以改变
isVisible();     
setVisible()/getVisible()    获取或者设置visible属性。默认是可见的，除了顶层框架默认是不可见

setSize();

java.awt.Window
toFront();     将窗口放到前面
toBack();     
isLocationByPlatform();
setLocationByPlatform(boolean b);  由平台选取一个合适位置，要在窗口显示之前被设置  


java.awt.Frame
isResizable();
setResizeble();
getTitle;/setTitle();
isUndecorated(); setUndecorated();    //undecorated意思是不被系统装饰。
//在窗口显示前调用这个方法
setExtendedState()/getExtendedState()   获取或设置窗口状态

java.awt.Toolkit
static Toolkit getDefaultToolkit();
Dimension getScreenSize();
Image getImage(String name);



框架大小
需要知道屏幕大小，用Toolkit类。这个类包含很多与本地窗口系统打交道的方法。
Toolkit kit = Toolkit.getDefaultToolkit();   //得到一个Toolkit对象
//getScreenSize方法以Dimension对象的形式返回屏幕的大小
Dimension screenSize = kit.getScreenSize();
//这个对象的两个共有实例变量保存着屏幕的宽度和高度。
int screenWidth =screenSize.width;
int screenHight =screenSize.higth;
setSize(screenWidth/2,screenHight/2);
setLocationByPlatform(true);



通常将框架大小设置为最大，用下列方法
frame.setExtendedState(Frame.MAXIMIZED_BOTH);


在组件中显示信息
通常并不将字符串直接显示在框架中，框架是放组件的容器。通常是将字符串放入组件中,然后再把组件放入框架中。

JFrame结构很复杂，结构是框架，根窗口，层级窗格，菜单栏（可选），内容窗格，玻璃窗格。
最关心的是内容窗格。在设计框架的时候要使用下列代码把所有组件添加到内容窗格中。
Container contentPane = frame.getContentPane();
Conponent c = ...;
contentPane.add(c);
也可以直接调用add方法，frame.add(c);就不需要使用上面的代码把组件添加到内容窗格了

这里要把绘制消息的组件放到框架里。要绘制一个组件，需要定义一个扩展
JComponent类的子类，并覆盖其中的paintComponent方法。
paintComponent方法有一个Graphics类型的参数，这个参数保存着用于绘制图像和文本的设置。例如字体的颜色。在java中，所有绘制都必须使用Graphics对象，包括绘制图案，图像和字体。
注意：不要自己调用paintComponent方法。这个方法会自己被调用。

显示文本是一种特殊绘制。在Graphics类有一个drawString方法，用于绘制字符串，g.drawString(text,x,y);


API总结
javax.swing.JFrame
Container getContentPane();  //返回JFrame的内容窗格对象
Component add();	//将一个组件添加到内容窗格中。所以用这个就不需要用上面的那个方法了

java.awt.Component
void repaint();	尽可能快的绘制组件
public void repaint(int x,int y,int width,int height);

javax.swing.JComponent
void paintComponent(Graphics g);		//覆盖这个方法来描述如何绘制自己的组件.记住，是paintComponent方法，不是paintComponents方法。

Graphics drawString(text,x,y);//绘制字符串



2D图形
要想使用2D绘制，需要获得Graphics2D类对象。这是Graphics类的子类。
paintComponent方法会自动获的一个Graphics2D类对象。只需要进行一次类型转换就可以了。
Line2D,Rectangle2D,Ellipse2D三个类分别画直线，长方形，椭圆。
画某个图形的方法：
Rectangle2D rect = ...;
g2.draw(rect);    //用Graphics2D里面的draw方法绘制图形


2D类采用浮点像素坐标，float，而不是double，因为float已经满足需求了.
但是有时候处理单精度有些不太方便，因为需要进行类型转换。
float f = 1.2; //Error    出错的原因是1.2是double，转换成float会丢失精度，编译器不允许这样。
解决办法是给浮点数后边加上F，
float f = 1.2F; //OK
//这里要注意，默认的浮点是double型的，就像上面的1.2，会默认为double型，
而float型的后面必须有后缀F 。这是前面介绍过的程序设计的概念。

下面的语句也会出错：
Rectangle2D r = ...
float f = r.getWidth(); //Error 。原因也一样，getWidth返回的是double。

由于后缀和类型转换有些麻烦，所以每个图形类有两个版本：一个是节省空间的float版本，一个是double类型的版本。
当创建Float版本，应该提供float型的数值，Double类型就提供double类型数值。
```
Rectangle2D.Double doubleRect = new Rectangle2D.Double(10.2,22.3,22.4,20.0);
Rectangle2D.Float floatRect = new Rectangle2D.Float(10.2F,22.3F,22.4F,20.0F);
```

//各有利弊，这本书选择第二个版本。
只有在*** 构造对象时 ***才需要记住图形类型，即是Double类型还是Float类型
因为Rectangle2D.Double和Rectangle2D.Float都是Rectangle2D的子类，
```
Rectangle2D doubleRect = new Rectangle2D.Double(10.2,22.3,22.4,20.0);
Rectangle2D floatRect = new Rectangle2D.Float(10.2F,22.3F,22.4F,20.0F);
```
虽然可以用单精度Float类型描述图像，但是返回值都是double型的。

通常得知两个矩形的两个点，但是这两个点并不一定是左上角和右下角。
如果已知四个顶点，应该用setFrameFromDiagonal方法表示。
```
Rectangle2D rect = new Rectangle2D.Double();
rect.setFrameFromDiagonal(px,py,qx,qy);
```
如果已知两个顶点，顶点分别是用Point2D类型的两个对象p，q表示，应该这样表示：
```
rect.setFrameFromDiagonal(p,q);
```

绘制图形不一定一定用顶点表示，有时候会利用图形的中心绘制。
例如绘制椭圆就有两种方法，一个是用外接矩形表示，一个是知道中心和一个顶点。
```
Ellipse2D e= new Ellipse2D.Double(centerX - width/2,centerY - height/2,width,height);  //绘制椭圆常用方法
```


绘制直线的两种方法
```
Line2D l = new Line2D.Double(start,end);     //给一个Point2D的两个点
Line2D l = new line2D.Double(startX,startY,endX,endY); //一对数值
```

### API总结
``` 
//返回闭合矩形的中心以及最大最小x，y坐标
java.awt.geom.RectangularShape 
double getCenterX()
double getCenterY()
double getMinX()
double getMinY()
double getMaxX()
double getMaxY()

java.awt.geom.Rectangle2D.Double
//给定左上角，宽和高
Rectangle2D.Double(double x,double y,double w,double h); 

java.awt.geom.Ellipse2D.Double
//给定左上角，宽和高的外接矩形
Ellipse2D.Double(double x,double y,double w,double h);

java.awt.geom.Line2D.Double
Line2D l = new Line2D.Double(start,end);     //给一个Point2D的两个点
//构造直线
Line2D l = new line2D.Double(startX,startY,endX,endY); //一对数值

```
### 颜色
Graphics2D类的setPaint方法绘制颜色,而不是填充颜色
```
g2.setPaint(Color.RED);
g2.drawString("Warning",100,100);
```

用fill填充一个封闭图形
```
g2.setPaint(Color.RED);
g2.fill(rect);
```

Color类用于定义颜色。有13个预定义颜色，RED就是一个
定制颜色可以用红，绿，蓝成分表示
```
g2.setPaint(new Color(0,128,128));
g2.drawString("Welcome",100,100);
```
背景颜色用Component的setBackground方法
```
MyComponent p = new MyComponent();
p.setBackground(Color.PINK);
```

setForeground();//绘制时默认颜色


### API总结
```
java.awt.Color
Color(int r,int g,int b)
Color getColor();

java.awt.Graphics
void setColor(Color r)
Paint getPaint()
void setPaint(Paint p)
void fill(Shape s)

java.awt.Component
Color getBackground()
Color setBackground(Color c)
Color getForeground()
void setForeground(Color c)
```

### 字体
跳过去了



###　图像
读取本地图像
String filename= "";
Image ig = ImageIO.read(new File(filename));
读取网络图片
String urlname= "";
Image ig = ImageIO.read(new URL(urlname));

用Graphics里的drawImage显示图像
g.drawImage(ig.x,y,null);

图像也没搞好,没弄清楚,以后再来看

