# ���
 ʲô�ǿ���أ����Ƕ��㴰�ڣ�û�а��������������еĴ��ڣ���
 ���ȶ���һ���ر�������ʱ����Ӧ����������������������˳�.
 �ڰ��������ܵĳ����в��ܹر�һ����ܾ��ó����˳���
 >��Ĭ�������ֻ�ǽ��������������������˳�

``` 
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
```
�򵥵Ĺ����ܳ����ǲ����Զ���ʾ�����ģ��������ǲ��ɼ��ġ������Ϳ����ڿ����ʾ֮ǰ
��������������
frame.setVisible(true);

awt��Swing��ܵļ̳в��.���Ƕ�����
Object->Component->Container->Window->Frame->JFrame

Swing����ǻ���awt��ܿ��������ģ����ǲ�û�д���awt��ܣ����������ṩ�˸���ǿ������.
��awt����,��һ����ΪFrame����,�����������㴰��.������Swing�汾��ΪJFame,����չ��Frame��.
�������Swing������� "J"��ͷ

Object->Component->Container->JComponent->JPanel

��ܶ�λ
JFrame��ܱ������ڸı䴰����۵ķ������٣��������ĳ������кܶ෽����
java.awt.Component��
setLocation(x,y)   ���ÿ������Ļ��λ�ã�
setBounds(x,y,width,height)  ����λ�úͳ��Ϳ�
setIconImage()���ߴ���ϵͳ�ڱ������������л����ڵ�λ����ʾ�ĸ�ͼ��
setTitle()  ���ñ���������
setResizable() ������ܴ�С�Ƿ���Ըı�
isVisible();     
setVisible()/getVisible()    ��ȡ��������visible���ԡ�Ĭ���ǿɼ��ģ����˶�����Ĭ���ǲ��ɼ�

setSize();

java.awt.Window
toFront();     �����ڷŵ�ǰ��
toBack();     
isLocationByPlatform();
setLocationByPlatform(boolean b);  ��ƽ̨ѡȡһ������λ�ã�Ҫ�ڴ�����ʾ֮ǰ������  


java.awt.Frame
isResizable();
setResizeble();
getTitle;/setTitle();
isUndecorated(); setUndecorated();    //undecorated��˼�ǲ���ϵͳװ�Ρ�
//�ڴ�����ʾǰ�����������
setExtendedState()/getExtendedState()   ��ȡ�����ô���״̬

java.awt.Toolkit
static Toolkit getDefaultToolkit();
Dimension getScreenSize();
Image getImage(String name);



��ܴ�С
��Ҫ֪����Ļ��С����Toolkit�ࡣ���������ܶ��뱾�ش���ϵͳ�򽻵��ķ�����
Toolkit kit = Toolkit.getDefaultToolkit();   //�õ�һ��Toolkit����
//getScreenSize������Dimension�������ʽ������Ļ�Ĵ�С
Dimension screenSize = kit.getScreenSize();
//����������������ʵ��������������Ļ�Ŀ�Ⱥ͸߶ȡ�
int screenWidth =screenSize.width;
int screenHight =screenSize.higth;
setSize(screenWidth/2,screenHight/2);
setLocationByPlatform(true);



ͨ������ܴ�С����Ϊ��������з���
frame.setExtendedState(Frame.MAXIMIZED_BOTH);


���������ʾ��Ϣ
ͨ���������ַ���ֱ����ʾ�ڿ���У�����Ƿ������������ͨ���ǽ��ַ������������,Ȼ���ٰ�����������С�

JFrame�ṹ�ܸ��ӣ��ṹ�ǿ�ܣ������ڣ��㼶���񣬲˵�������ѡ�������ݴ��񣬲�������
����ĵ������ݴ�������ƿ�ܵ�ʱ��Ҫʹ�����д�������������ӵ����ݴ����С�
Container contentPane = frame.getContentPane();
Conponent c = ...;
contentPane.add(c);
Ҳ����ֱ�ӵ���add������frame.add(c);�Ͳ���Ҫʹ������Ĵ���������ӵ����ݴ�����

����Ҫ�ѻ�����Ϣ������ŵ�����Ҫ����һ���������Ҫ����һ����չ
JComponent������࣬���������е�paintComponent������
paintComponent������һ��Graphics���͵Ĳ���������������������ڻ���ͼ����ı������á������������ɫ����java�У����л��ƶ�����ʹ��Graphics���󣬰�������ͼ����ͼ������塣
ע�⣺��Ҫ�Լ�����paintComponent����������������Լ������á�

��ʾ�ı���һ��������ơ���Graphics����һ��drawString���������ڻ����ַ�����g.drawString(text,x,y);


API�ܽ�
javax.swing.JFrame
Container getContentPane();  //����JFrame�����ݴ������
Component add();	//��һ�������ӵ����ݴ����С�����������Ͳ���Ҫ��������Ǹ�������

java.awt.Component
void repaint();	�����ܿ�Ļ������
public void repaint(int x,int y,int width,int height);

javax.swing.JComponent
void paintComponent(Graphics g);		//�������������������λ����Լ������.��ס����paintComponent����������paintComponents������

Graphics drawString(text,x,y);//�����ַ���



2Dͼ��
Ҫ��ʹ��2D���ƣ���Ҫ���Graphics2D���������Graphics������ࡣ
paintComponent�������Զ����һ��Graphics2D�����ֻ��Ҫ����һ������ת���Ϳ����ˡ�
Line2D,Rectangle2D,Ellipse2D������ֱ�ֱ�ߣ������Σ���Բ��
��ĳ��ͼ�εķ�����
Rectangle2D rect = ...;
g2.draw(rect);    //��Graphics2D�����draw��������ͼ��


2D����ø����������꣬float��������double����Ϊfloat�Ѿ�����������.
������ʱ����������Щ��̫���㣬��Ϊ��Ҫ��������ת����
float f = 1.2; //Error    �����ԭ����1.2��double��ת����float�ᶪʧ���ȣ�������������������
����취�Ǹ���������߼���F��
float f = 1.2F; //OK
//����Ҫע�⣬Ĭ�ϵĸ�����double�͵ģ����������1.2����Ĭ��Ϊdouble�ͣ�
��float�͵ĺ�������к�׺F ������ǰ����ܹ��ĳ�����Ƶĸ��

��������Ҳ�����
Rectangle2D r = ...
float f = r.getWidth(); //Error ��ԭ��Ҳһ����getWidth���ص���double��

���ں�׺������ת����Щ�鷳������ÿ��ͼ�����������汾��һ���ǽ�ʡ�ռ��float�汾��һ����double���͵İ汾��
������Float�汾��Ӧ���ṩfloat�͵���ֵ��Double���;��ṩdouble������ֵ��
```
Rectangle2D.Double doubleRect = new Rectangle2D.Double(10.2,22.3,22.4,20.0);
Rectangle2D.Float floatRect = new Rectangle2D.Float(10.2F,22.3F,22.4F,20.0F);
```

//�������ף��Ȿ��ѡ��ڶ����汾��
ֻ����*** �������ʱ ***����Ҫ��סͼ�����ͣ�����Double���ͻ���Float����
��ΪRectangle2D.Double��Rectangle2D.Float����Rectangle2D�����࣬
```
Rectangle2D doubleRect = new Rectangle2D.Double(10.2,22.3,22.4,20.0);
Rectangle2D floatRect = new Rectangle2D.Float(10.2F,22.3F,22.4F,20.0F);
```
��Ȼ�����õ�����Float��������ͼ�񣬵��Ƿ���ֵ����double�͵ġ�

ͨ����֪�������ε������㣬�����������㲢��һ�������ϽǺ����½ǡ�
�����֪�ĸ����㣬Ӧ����setFrameFromDiagonal������ʾ��
```
Rectangle2D rect = new Rectangle2D.Double();
rect.setFrameFromDiagonal(px,py,qx,qy);
```
�����֪�������㣬����ֱ�����Point2D���͵���������p��q��ʾ��Ӧ��������ʾ��
```
rect.setFrameFromDiagonal(p,q);
```

����ͼ�β�һ��һ���ö����ʾ����ʱ�������ͼ�ε����Ļ��ơ�
���������Բ�������ַ�����һ��������Ӿ��α�ʾ��һ����֪�����ĺ�һ�����㡣
```
Ellipse2D e= new Ellipse2D.Double(centerX - width/2,centerY - height/2,width,height);  //������Բ���÷���
```


����ֱ�ߵ����ַ���
```
Line2D l = new Line2D.Double(start,end);     //��һ��Point2D��������
Line2D l = new line2D.Double(startX,startY,endX,endY); //һ����ֵ
```

### API�ܽ�
``` 
//���رպϾ��ε������Լ������Сx��y����
java.awt.geom.RectangularShape 
double getCenterX()
double getCenterY()
double getMinX()
double getMinY()
double getMaxX()
double getMaxY()

java.awt.geom.Rectangle2D.Double
//�������Ͻǣ���͸�
Rectangle2D.Double(double x,double y,double w,double h); 

java.awt.geom.Ellipse2D.Double
//�������Ͻǣ���͸ߵ���Ӿ���
Ellipse2D.Double(double x,double y,double w,double h);

java.awt.geom.Line2D.Double
Line2D l = new Line2D.Double(start,end);     //��һ��Point2D��������
//����ֱ��
Line2D l = new line2D.Double(startX,startY,endX,endY); //һ����ֵ

```
### ��ɫ
Graphics2D���setPaint����������ɫ,�����������ɫ
```
g2.setPaint(Color.RED);
g2.drawString("Warning",100,100);
```

��fill���һ�����ͼ��
```
g2.setPaint(Color.RED);
g2.fill(rect);
```

Color�����ڶ�����ɫ����13��Ԥ������ɫ��RED����һ��
������ɫ�����ú죬�̣����ɷֱ�ʾ
```
g2.setPaint(new Color(0,128,128));
g2.drawString("Welcome",100,100);
```
������ɫ��Component��setBackground����
```
MyComponent p = new MyComponent();
p.setBackground(Color.PINK);
```

setForeground();//����ʱĬ����ɫ


### API�ܽ�
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

### ����
����ȥ��



###��ͼ��
��ȡ����ͼ��
String filename= "";
Image ig = ImageIO.read(new File(filename));
��ȡ����ͼƬ
String urlname= "";
Image ig = ImageIO.read(new URL(urlname));

��Graphics���drawImage��ʾͼ��
g.drawImage(ig.x,y,null);

ͼ��Ҳû���,ûŪ���,�Ժ�������

