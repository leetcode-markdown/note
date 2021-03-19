# 2021.2.25

* **结构体对齐**

  *linux结构体自动对齐，windows需要此操作*

  ```
  #pragma pack(1)
  
  struct node_package {
    uint16_t  package_Head;
    uint8_t   package_CT;
    uint8_t   nowPackageNum;
    uint16_t  packageFirstSampleAngle;
    uint16_t  packageLastSampleAngle;
    uint16_t  checkSum;
    PackageNode  packageSample[PackageSampleMaxLngth];
  } __attribute__((packed)) ;
  
  #pragma pack() //取消字节对齐
  windows两者缺一不可，linux只需要加上__attribute__((packed))宏。

  方法二:
  #pragma pack(push,1)
  struct test1 {
    char a;
    int  b;
  }
  #pragma pack(pop)
  //pragma pack(pop) 取消字节对齐
  ```
  
* 继承qoject时，构造函数总要加上QObject(parent),代表将子类接收到的参数也传给父类。

* 定义全局变量时，最好定义在.cpp文件中，头文件中用extern 引用，这样引用头文件后，就不会多次重定义。

* 宏定义，##连接符，#字义转换符，#,##字符只能在预编译时使用，不能用到逻辑中

* 使用goto时，变量必须先声明，不能在goto后面声明变量

* sizeof计算缓冲区长度

  ```
  char a[30];
  sizeof(a) //30
  sizeof(*a)  //1
  sizeof(&a)  //8
  sizeof(a+1)  //8
  ```

* 大端模式和小端模式

  ```
  大端是高位在前，x86是小端模式,即主机地址是小端模式
  
  大小端转换
  uint32_t htonl(uint32_t hostlong);
  uint16_t htons(uint16_t hostshort);
  uint32_t ntohl(uint32_t netlong);
  uint16_t ntohs(uint16_t netshort);
  htonl 表示 host to network long ，用于将主机 unsigned int 型数据转换成网络字节顺序；
  htons 表示 host to network short ，用于将主机 unsigned short 型数据转换成网络字节顺序；
  ntohl、ntohs 的功能分别与 htonl、htons 相反。
  
  linux包含头文件
  #include <sys/socket.h>
  #include <netinet/in.h>
  #include<arpa/inet.h>
  
  windows包含头文件
  #include <WS2tcpip.h>
  
  ```

  