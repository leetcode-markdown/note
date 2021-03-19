# Qt  API



---

记录一些不常见的API函数

----



* QCoreApplication 和 QApplication 区别

  > QApplication 是带Gui的，QCoreApplication 是不带的，

* QApplication

  | 函数名                                     | 解析           | 备注                                                     |
  | ------------------------------------------ | -------------- | -------------------------------------------------------- |
  | setStyle(QStyleFactory::create("Fusion")); | 设置界面的风格 | https://tangxing.blog.csdn.net/article/details/111152257 |
  |                                            |                |                                                          |
  |                                            |                |                                                          |

* QSetting

  | 函数名                                                       | 解析                                                         | 备注                                                    |
  | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------- |
  | QSettings::beginGroup                                        | 给当前的group里由QSettings指定的所有键(key)，自动附上当前的group前缀,即查询时附在当前键后面 | https://blog.csdn.net/waangyan/article/details/69542724 |
  | QSettings::value(const QString &key, const QVariant &defaultValue = QVariant()) const | 查询当前键的值，第一个key为要查询的参数，第二个键为默认值    |                                                         |
  | setWindowModality(Qt::WindowModal)                           | 此属性保存哪些窗口被模式窗口小部件阻止 此属性仅对Windows有意义。 模态窗口小部件可防止其他窗口中的窗口小部件获得输入。 此属性的值控制在小部件可见时哪些窗口被阻止 |                                                         |
| QStandardPaths                                               | 获取各种目录（桌面，文档，用户等）                           |                                                         |
  | QDir                                                         | 对目录的操作(QDir::exists,mkdir(创建))                       |                                                         |
  | QSettings                                                    | 对配置文件的操作                                             |                                                         |
  | QLocale().country()                                          | 返回所在国家的枚举对象                                       |                                                         |
  
  ---
  
  **Qt全局函数**
  
  | 名称       | 解析                                                         | 备注 |
  | ---------- | ------------------------------------------------------------ | ---- |
  | Q_ASSERT_X | qt类型断言，当不符合预期结果时，让程序退出，并弹出系统报错框 |      |
  |            |                                                              |      |
  |            |                                                              |      |
  
* QTimer

  | 名称       | 解析                                                     | 备注 |
  | ---------- | -------------------------------------------------------- | ---- |
  | singleShot | 不需要处理事件循环和创建QTimer对象，可以让其循环发射信号 |      |

* QToolButton 和 QPushButton

  > QToolButton 不显示文本，只显示图标，若涉及到背景图片的操作时，用QToolButton
  
* ### QFont("Times",18,QFont::Bold)

  > 用times 字体，大小为18，加粗
  
* QDockWidget

  > 工具栏窗口，可以移动，悬浮，隐藏
  
* QFuture

  > QFuture允许线程针对一个或多个结果进行同步，这些结果将在以后的某个时间点准备就绪。结果可以是具有默认构造函数和副本构造函数的任何类型。如果在调用result（），resultAt（）或results（）函数时结果不可用，则QFuture将等待，直到结果变为可用。您可以使用isResultReadyAt（）函数来确定结果是否准备就绪

