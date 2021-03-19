# C++ 宏

-----

* ## __declspec(dllexport)与__declspec(dllimport)

* > 区别
  >
  > ​    他们都是DLL内的关键字，即导出与导入。他们是将DLL内部的类与函数以及数据导出与导入时使用的。
  >
  >    dllexport是在这些类、函数以及数据的申明的时候使用。用他表明这些东西可以被外部函数使用，即（dllexport）是把 DLL中的相关代码（类，函数，数据）暴露出来为其他应用程序使用。使用了（dllexport）关键字，相当于声明了紧接在（dllexport）关键字后面的相关内容是可以为其他程序使用的。
  >
  >    dllimport是在外部程序需要使用DLL内相关内容时使用的关键字。当一个外部程序要使用DLL 内部代码（类，函数，全局变量）时，只需要在程序内部使用（dllimport）关键字声明需要使用的代码就可以了，即（dllimport）关键字是在外部程序需要使用DLL内部相关内容的时候才使用。（dllimport）作用是把DLL中的相关代码插入到应用程序中。
  >
  >    _declspec(dllexport)与_declspec(dllimport)是相互呼应，只有在DLL内部用dllexport作了声明，才能在外部函数中用dllimport导入相关代码。