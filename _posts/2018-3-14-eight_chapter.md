---
layout: post
title: 第八章——时间处理
published: true
tags: [core_java]
---

## 事件概述
面向对象的语言，都将事件的信息封装在事件对象中（event object），所有事件对象都派生于java.util.EventObject类。每个事件类型还有子类，如ActionEvent，WindowEvent。

不同的事件源(如按钮，滚动条)可以产生不同类型的事件，例如按钮可以发送ActionEvent对象，而窗口可以发送WindowEvent对象。

事件处理机制概要：
* 监听器对象是实现了特定监听器接口的类的实例。 //监听器是一个类的实例？？？
* 事件源是一个能够注册监听器对象并发送事件对象的对象。
* 当事件发生时，事件源将事件对象传递给所有注册的监听器。
* 监听器对象将利用事件中的信息决定如何对事件做出响应。

注意:
***事件源将  事件对象   传递给注册的监听器***

监听器示例：
```
ActionListener listener = ...;
JButton button = new JButton("OK");
button.addActionListener(listener);  //添加一个监听这个事件源的监听器
```


为了实现ActionListener接口(监听器对象)，监听器类必须有一个actionPerformed的方法。该方法接受一个ActionEvent对象参数。

```
class Mylistener implements ActionListener{
    ...
    public void actionPerformed(ActionEvent event){
        //reaction to button goed here
        ... }
}
```

只要用户点击按钮，button对象就会创建一个ActionEvent对象，然后调用listener.actionPerformed(event)传递事件对象。

## 实例分析

下面显示了如何将按钮添加到面板上：
```
class MyFrame extends JFrame{
    .....

 JButton redButton = new JButton("red");

//JPanel是可以包含其他组件的容器。这里相当于添加了一个包含按钮的容器
JPanel buttonPanel = new JPanel();

//把按钮添加到按钮容器中
buttonPanel.add(redButton);

//把容器添加到框架里面
add(buttonPanel);

}
```


然后需要监听这些按钮的事件
``` 
        //如何监听呢？很简单，往按钮里添加一个监听对象就行了.怎么实现监听对象呢？
        // 实现一个ActionListener接口的类，包含actionPerformed方法.
        //public void actionPerformed(ActionEvent event);

        //实现一个监听类的对象,监听类就是监听到事件后执行什么行为
        ColorAction redAction = new ColorAction(Color.RED);

        redButton.addActionListener(redAction);

    //这实现一个监听接口的类，就是监听到事件时执行什么行为.这里是当监听到事件时背景变成红色
    private class ColorAction implements ActionListener {
        private Color backgroundColor;
        public ColorAction(Color c) {
            backgroundColor = c;
        }

        public void actionPerformed(ActionEvent event) {
            buttonPanel.setBackground(backgroundColor);
        }

    }
```


## API总结
```
javax.swing.JButton

JButton(String label)
JButton(Icon icon)
JButton(String label,Icon icon)
构造一个按钮。

java.awt.Container
Component add(Component c)
将组件c添加到容器中

java.swing.ImageIcon
ImageIcon(String filename)
构造一个图标
```

