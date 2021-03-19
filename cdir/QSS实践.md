# QSS实践:

* QComboBox

  ```css
  QComboBox {
      border: 0;
      border-radius: 2;  //边框圆角，以像素为单位
      background-color: @color01; 
      padding: 4 0 4 10; ////组合框内的文本内容
      font-size: 11pt;
      color: @color05;
      min-width: 20;  //组合框的最小宽度
  }
  
  ```
* QComboBox::drop-down {   //下拉框的按钮
        background-color: @color01; //背景颜色为
        subcontrol-position: top right; //下拉提示按钮在组合框的右上角
        width: 14;
        padding: 0 5;
        color: @color05; 

  ```css
    border-left-width: 1px;
    border-left-color: @color01; //下拉按钮和左边文本框的间隔的颜色，特别小，
    border-left-style: solid;
    image: url(:/static/themes/default/img/down-arrow.png); //替换下拉选择框右边角落按钮的图片 
    border-top-right-radius: 2;
    border-bottom-right-radius: 2;
  ```

  

*  [Qt 布局](https://www.cnblogs.com/findumars/p/8001443.html)

  ```css
  border:1px solid gray  //宽度为一个像素，solid 为实线， gray 为灰色
  ```

* # [QT学习之QImage::scaled](https://www.cnblogs.com/qixianyu/p/6891054.html)

  QT中图片的比例变换，为了适应控件的大小，采用QImage、QPixmap等绘图设备类提供的scaled()函数，下面是Qt文档对于scaled()函数介绍：

  函数原型：

  QImage QImage::scaled ( int width, int height,  Qt::AspectRatioMode aspectRatioMode = Qt::IgnoreAspectRatio,  Qt::TransformationMode transformMode = Qt::FastTransformation ) **const**  

  This is an overloaded function.

  Returns a copy of the image scaled to a rectangle with the given *width* and *height* according to the given A*spectRatioMode* and T*ransformMode*.

  If either the *width* or the *height* is zero or negative, this function returns a null image.

  这是一个重载函数，按照指定的宽和高，根据纵横比（Aspect Ratio）模式和转换模式从原有图像返回一个经过比例转换的图像，如果宽高为0，返回一个空图像

  所以，获取控件的改变后的宽高，就能设定图像转换的宽高转换比例，用scaled()的返回重新进行绘图即可自适应窗口。

| 选择器     | 示例                      | 说明                                                         |
| :--------- | :------------------------ | :----------------------------------------------------------- |
| 通用选择器 | *                         | 匹配所有部件                                                 |
| 类型选择器 | QPushButton               | 匹配QPushButton及其子类的实例                                |
| 属性选择器 | QPushButton[flat=”false”] | 匹配QPushButton中flat属性为false的实例。可以用此选择器来测试任何支持`QVariant::toString()`的属性，此外，支持特殊的类属性、类名称。此选择器也可以用来测试动态属性（参考助手：`Qt Style Sheets Examples`中`Customizing Using Dynamic Properties`部分）。还可以使用~=替换=，测试QStringList类型的属性是否包含给定的QString。 警告：如果Qt属性值在设置样式之后更改，那么可能需要强制重新计算样式。实现的一个方法是取消样式，然后重新设置一遍。 |
| 类选择器   | .QPushButton              | 匹配QPushButton的实例，但不包含子类。相当于*[class~=”QPushButton”]。 |
| ID选择器   | QPushButton#okButton      | 匹配所有objectName为okButton的QPushButton实例。              |
| 后代选择器 | QDialog QPushButton       | 匹配属于QDialog后代（孩子，孙子等）的QPushButton所有实例。   |
| 子选择器   | QDialog > QPushButton     | 匹配属于QDialog直接子类的QPushButton所有实例。               |