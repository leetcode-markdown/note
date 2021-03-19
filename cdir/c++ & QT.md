# c++ & QT

## 2020.11.19

-------

----

* 槽函数和信号

  [qRegisterMetaType]()

  ```
  注意：槽函数和信号的参数只能传递通用类型，若要传输自己定义的类或者QVector等类型，则需要用QVarient,qRegisterMetaType进行注册封装。
  ```

* [windows下 QT中文显示乱码](https://www.cnblogs.com/herd/p/10879520.html)

  ```c++
  #if _MSC_VER >= 1600
  #pragma execution_character_set("utf-8")
  #endif
  ```

* Q_DECL_IMPORT 和 Q_DECL_EXPORT

  > QD

* [QT pro文件](https://blog.csdn.net/liang19890820/article/details/51774724)

  | 名称                    | 用法                                                         | 说明                                                         |
  | ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | DEFINES                 | DEFINES += BIL_LIB                                           | 可以用作定义宏，即定义BIL_LIB这个宏                          |
  | TARGET                  | TAGET = test                                                 | 定义生成的目前程序或库名                                     |
  | TEMPLATE                | TEMPLATE=lib 或者 subdirs 或者app                            | 指定生成动态库,后面表明qt跨目录，由多个子项目构成，后面表示生成应用程序 |
  | DESTDIR                 | DESTDIR=./bin                                                | 生成程序的存放路径                                           |
  | win32{}  unix{}         | unix {#表示Linux环境的特殊设置，这个大括号不能单独放在下一行，否则编译会报错<br/>    target.path = /usr/lib<br/>    INSTALLS += target<br/>} | 不同环境的设置                                               |
  | target.path 和 INSTALLS | target.path = /usr/lib<br/>    INSTALLS += target<br/>       | 指的是make install的安装路径                                 |
  | $$PWD 和$$OUT_PWD       |                                                              | pwd表示的是pro文件的路径,out_pwd是生成程序的路径             |
  | QMAKE_CXXFLAGS          |                                                              | 相当于CXX_FLAGS，可以往后面加编译参数                        |
  | DEPENDPATH              |                                                              | 应用程序所依赖的搜索路径                                     |
  | VPATH                   |                                                              | 寻找补充文件的搜索路径                                       |
  | DEF_FILE                |                                                              | 应用程序链接的.def文件，仅支持Windows。                      |
  | RC_FILE                 |                                                              | 应用程序的资源文件，                                         |
  | RES_FILE                |                                                              | 应用程序链接的资源文件，仅支持Windows。                      |
  | contains                |                                                              | contains( variablename, value )如果value存在于一个被叫做variablename的变量的值的列表中，那么这个作用域中的设置将会被处理。例如： |
  | depends                 | plugins.depends = lib                                        | plugins 的依赖模块为libs模块                                 |

  

* QT 的系统标准路径库 QStandardPaths

  > QStandardPaths::writableLocation()  获取系统标准路径，如图片，下载，桌面，文档等路径。

* qt等待(qApp->processEvents())

  > 处理下事件。比如有个事务处理比较耗时间，你可以在中间不时地processEvents()下，这样好让界面处理一下各种事件，避免看上去无反应像死掉一样。

* qInstallMessageHandler

  > 输出重定向，可以将qDebug() 等的调试输出，重定向到文件中

* QSplashScreen 开始界面类

  > 程序启动时显示的开始界面

* QLatin1String类对US-ASCII/Latin-1编码的字符串进行了简单封装，可理解为关于const char*的一个浅封装。

* QSharedPointter 为qt智能指针，可以自动释放，不同的是他可以反复拷贝，一直到引用数为0才释放，

* qgetenv  返回该环境变量的值

* **在Qt中，当一个对象被移到另一个线程时，他的所有子对象也会一并转移到另外那个线程。**

* **在Qt中，如果要切换对象的线程，不能到了目标线程里再调用moveToThread,此举会导致切换线程失败。**

* **由此可见Qt中，子对象不能脱离父对象，单独切换到与父对象不同的线程中。**

* **对于Qt子对象而言，不能在父对象删除后，再删除自己。因为父对象析构时，会删除所有的子对象，此时子对象再删除，会引起二次析构。**

  **所以如果子对象要切换到另一个线程或者避免被父对象删除，则需要调用setParent(NULL),解除父子关系。**
  
* Qt 使用moveToThread时，一定不能使用Qt::DirectionConnect, 不然槽函数就在当前线程中运行。

* setProperty("flag", "menu")，setProperty可以给对象自定义属性，用来区分对象

* 在线程的创建的资源永远停留在线程中，在某一线程中创建的资源，不要跨线程使用，会崩溃

* >
  >
  >Qt使用PRE_TARGETDEPS变量来存储静态链接库的依赖项.每次构建应用程序时,它都会强制您的库重新链接.
  >如果您没有指定此变量并且更新并重建库,则程序仍将使用旧库.
  >
  >对于您的问题,如果您使用静态库,您应该(几乎)始终使用LIB和PRE_TARGETDEPS.

* qt arg, 当出现不确定的字节数，并需要字节数填充时，可以用arg(QString,int fileWidth,QChar),fileWidth 表示QString 的长度，不足用QChar填充

* QT语法糖

  | 函数(宏)                                           | 作用                                             | 备注                                           |
  | -------------------------------------------------- | ------------------------------------------------ | ---------------------------------------------- |
  | tr是为了国际化，一般不要用tr，中间经过了很多转换， | 如何一段语句会被翻译成很多语言，就用tr将其括起来 | https://www.cnblogs.com/lsgxeva/p/7814072.html |
  |                                                    |                                                  |                                                |
  |                                                    |                                                  |                                                |
  |                                                    |                                                  |                                                |
  |                                                    |                                                  |                                                |
  |                                                    |                                                  |                                                |
  |                                                    |                                                  |                                                |
  |                                                    |                                                  |                                                |
  |                                                    |                                                  |                                                |




*-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------*

### 2、指定库文件路径PWD/OUT_PWD/_PRO_FILE_/_PRO_FILE_PWD_

- **PWD**

指的是当前正在解析的.pro文件的目录的完整路径。 在编写支持影子构建的项目文件时，PWD很有用。

message($$PWD)

- **OUT_PWD**

指的是qmake生成的Makefile的目录的完整路径。即构建目录，例如build-??-Desktop_Qt_5_12_8_MSVC2017_64bit-Debug

message($$OUT_PWD)

- **_PRO_FILE_**

正在使用的项目文件的路径。

message($$_PRO_FILE_)

- **_PRO_FILE_PWD_**

包含目录的路径，该目录包含正在使用的项目文件。

message($$_PRO_FILE_PWD_)



*-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------*



### 1、指定临时文件

Qt Creator默认情况下把所有的编译中间文件都生成到debug和release文件夹里。可以在.pro文件中加入：

```
MOC_DIR = temp/moc



RCC_DIR = temp/rcc



UI_DIR = temp/ui



OBJECTS_DIR = temp/obj
```

这样，编译时生成的临时文件就按不同类型分类放到项目下的temp文件夹中了。





*-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------*

参考bai了C++ Primer Plus第五duzhi中文dao P8
C++实现zhuan 源代码的shu扩展名
UNIX C、权cc、cxx、c
GNU C++ C、cc、cxx、cpp、c++
Borland C++ Cpp
Microsoft Visual C++ cpp、cxx、cc

