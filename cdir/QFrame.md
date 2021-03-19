## QFrame

* **QFrame是带边框部件的基类**
* 主要功能是实现不同的边框效果，这主要是由边框形状（Shape）和 边框阴影（Shadow）组合来形成的。
* lineWidth是边框边界线的宽度，midLineWidth是在边框中额外插入的一条线的宽度，这条线的作用是为了实现3D效果。



## QFont

```c++
QFont font;
font.setFamily("华文行楷"); //设置字体
font.setPointSize(20);    //设置字体大小
font.setBold(true);      //加粗
font.setItalic(true)     //斜体
```



## QPixmap 和 QMovie

```
setPixmap(QPixmap("123.png")); //设置图片
QMovie movie("E:\123.gif");
setMovie(movie);
movie->start();
```



## QLayout

* QSizePolicy

   *大小策略*

## 设置tab键顺序

  

```
setTabOrder(QWidget* a,QWidget* b) //a在b前面
```

