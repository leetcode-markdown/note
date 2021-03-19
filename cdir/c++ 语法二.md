# c++ 语法二

2020.11.2~2020.11.6

---

---

## 2020.11.2

* linux 线程

  ```c++
  int pthread_join(pthread_t thread, void **retval);
  //pthread_join()函数，以阻塞的方式等待thread指定的线程结束。当函数返回时，被等待线程的资源被收回。如果线程已经结束，那么该函数会立即返回。并且thread指定的线程必须是joinable的
  //*参数* ：thread: 线程标识符，即线程ID，标识唯一线程。retval: 用户定义的指针，用来存储被等待线程的返回值。
  //*返回值* ： 0代表成功。 失败，返回的则是错误号.
  
  int pthread_cancel(pthread_t thread)
  //pthread_cancel，是计算机语言，它发送终止信号给thread线程，如果成功则返回0，否则为非0值。
  //若是在整个程序退出时，要终止各个线程，应该在成功发送 CANCEL 指令后，使用 pthread_join 函数，等待指定的线程已经完全退出以后，再继续执行；否则，很容易产生 “段错误”
      
  #include <pthread.h>
  int pthread_create(pthread_t *restrict tidp,
                     const pthread_attr_t *restrict attr,
                     void *(*start_rtn)(void), 
                     void *restrict arg);
  //tidp 随便传入一个pthread_t就行，线程初始化成功后，会填充tidp的值，
  //TODO:pthread_create 会启动线程，
  int pthread_cancel(pthread_t thread)
  发送终止信号给thread线程，如果成功则返回0，否则为非0值。发送成功并不意味着thread会终止。
  ```

* 关键字修饰

  | 关键字 | 用法                    | 作用                                        |
  | ------ | ----------------------- | ------------------------------------------- |
  | const  | 1.void  A(int a) const; | 对象的成员在函数中不可修改，隐性const this. |

* 函数

  ```
  成员函数:无论静态函数还是非静态函数,都是属于类的(这一点与数据成员的静态非静态不同),对象并不拥有函数的拷贝.两者的区别在于:非静态的函数由类对象(加.或指针加->;)调用,这时将向函数传递this指针.而静态函数由类名(::)(或对象名.)调用,但静态函数不传递this指针,不识别对象个体,所以通常用来对类的静态数据成员操作.
  类的静态成员(变量和方法)属于类本身，在类加载的时候就会分配内存，可以通过类名直接去访问；非静态成员（变量和方法）属于类的对象，所以只有在类的对象产生（创建类的实例）时才会分配内存，然后通过类的对象（实例）去访问。
  
  在一个类的静态成员中去访问其非静态成员之所以会出错是因为在类的非静态成员不存在的时候类的静态成员就已经存在了，访问一个内存中不存在的东西当然会出错。
  
  C++会区分两种类型的成员函数：静态成员函数和非静态成员函数。这两者之间的一个重大区别是，静态成员函数不接受隐含的this自变量。所以，它就无法访问自己类的非静态成员。
  ```

* new的进阶用法

  [new](https://www.cnblogs.com/lustar/p/10717502.html)

  在一个已经分配好的内存指针上调用构造函数

* **_alloca**是在栈(stack)上申请空间,该变量离开其作用域之后被自动释放，无需手动调用释放函数。

* ioctl

  [tiocmget](https://blog.csdn.net/aba13579/article/details/20775145)

  ```
   ioctl 是用来设置硬件控制寄存器，或者读取硬件状态寄存器的数值之类的。而read,write 是把数据丢入缓冲区，硬件的驱动从缓冲区读取数据一个个发送或者把接收的数据送入缓冲区。
   ioctl(keyFd, FIONREAD, &b)
  
  得到缓冲区里有多少字节要被读取，然后将字节数放入b里面。
  
   tty 驱动的 tiocmget 和 tiocmset 函数
  
   对 TIOCMGET、TIOCMSET、TIOCMBIC 和 TIOCMBIS IO 控制命令的调用将被
   tty 核心转换为对 tty 驱动 tiocmget()函数和 tiocmset()函数的调用，TIOCMGET 对应
   tiocmget()函数，TIOCMSET、TIOCMBIC 和 TIOCMBIS  对应 tiocmset()函数
  ```

* as 

  ```
    lidar_ans_header *header,
    uint8_t  recvBuffer[sizeof(lidar_ans_header)]; //雷达接收数据头
    uint8_t  *headerBuffer = reinterpret_cast<uint8_t *>(header);
    //之所以可以这样转换，因为headerBuffer,
  ```

## 2020.11.4

* 运算符优先级

  ```
  在同一语句中，若&& 和 ||同时存在，且没有用（）强行注明谁先执行，&&会比||先执行。
  ```

* stl函数

  ```
  accumulate(data.begin(),data.end(),42); //代表从42开始累加求值。begin和end代表范围。
  ```


## 2020.11.5

* [三目运算符](https://www.it1352.com/490714.html)

  ```
  多个三目运算符的运算顺序
  ```

* [socket](https://www.cnblogs.com/jiangzhaowei/p/8261174.html)

  ```c++
  **gethostbyname //通过域名获取ip地址等详细信息 *http://c.biancheng.net/view/2357.html*
    用法:struct hostent *gethostbyname(const char *hostname);
    servaddr.sin_addr.s_addr = htonl(INADDR_ANY);//IP地址设置成INADDR_ANY,让系统自动获取本机的IP地址
  **connect超时处理:/** https://www.cnblogs.com/alantu2018/p/8469502.html              https://blog.csdn.net/peng314899581/article/details/79651616**/
  **send发送数据://https://baike.baidu.com/item/send/13483552#2
  **sendto:是一个计算机函数，指向一指定目的地发送数据，sendto()适用于发送未建立连接的UDP数据包 （参数为        SOCK_DGRAM）
  **recv: //https://baike.baidu.com/item/recv%28%29?fromtitle=recv&fromid=17200658
     注：对socket用fcntl设置阻塞，并不会影响到 recv和send ，这两个函数的最后一个参数flags可以用来设置发送    或接收的模式
  ```

* char 指针

  ```
  %s :表示从给定的地址开始，向后查找，一直到找到\0,没有\0就会错误。
  * ，[]: 这两个字符都是取给定地址存放的值。
  ```

## 2020.11.6

* getpeername

  ```
  对于这两个函数，如果函数调用成功，则返回0，如果调用出错，则返回-1。
  使用这两个函数，我们可以通过套接字描述符来获取自己的IP地址和连接对端的IP地址，如在未调用bind函数的TCP客户端程序上，可以通过调用getsockname()函数获取由内核赋予该连接的本地IP地址和本地端口号，还可以在TCP的服务器端accept成功后，通过getpeername()函数来获取当前连接的客户端的IP地址和端口号。
  ```

* [setsockopt](https://blog.csdn.net/chq1005613740/article/details/100727031)

  ```
  功能描述：
          获取或者设置与某个套接字关联的选 项。选项可能存在于多层协议中，它们总会出现在最上面的套接字层。当操作套接字选项时，选项位于的层和选项的名称必须给出。为了操作套接字层的选项，应该 将层的值指定为SOL_SOCKET。为了操作其它层的选项，控制选项的合适协议号必须给出。例如，为了表示一个选项由TCP协议解析，层应该设定为协议 号TCP。
  ```

* c 变量名转换成字符串

  ```c++
  #define  valname(c)  (#c);
  加#可以实现。如：
  valname(test.name); //会输出字符串 "test.name"
  ```

* [strtok](https://blog.csdn.net/u012005313/article/details/69595698)

  ```c++
  #include <stdio.h>
  #include <stdlib.h>
  #include <string.h>
  /**
  *第一次传入str,后面传入NULL，每次函数返回的值都是拆分的那段
  **/
  int main(int argc, char* argv[]) {
      char str[] = "- This, a sample string.";
      char * pch;
      printf("Splitting string \"%s\" into tokens:\n", str);
      pch = strtok(str, " ,.-");
      while (pch != NULL)
      {
          printf("%s\n", pch);
          pch = strtok(NULL, " ,.-");
      }
  
      printf("str: %s\n", str);
  
      system("pause");
      return 0;
  }
  ```

* [sprintf](https://blog.csdn.net/qq_37059136/article/details/80278742)

  ```
  sprintf是将格式化输出到字符串
  ```

* [errno](https://baike.baidu.com/item/errno)

  ```
  errno 是记录系统的最后一次错误代码。代码是一个int型的值，在errno.h中定义。查看错误代码errno是调试程序的一个重要方法。当linux C api函数发生异常时,一般会将errno变量(需include errno.h)赋一个整数值,不同的值表示不同的含义,可以通过查看该值推测出错的原因。在实际编程中用这一招解决了不少原本看来莫名其妙的问题。
  ```

* [sscanf](sscanf(buf, "%[^=]=%[^=]", recvDesc, recvValue))

  ```
  sscanf(buf, "%[^=]=%[^=]", recvDesc, recvValue);//将buf按第二个参数的格式将结果输出到后面的几个参数中，返回值为成功返回的参数个数。
  ```

## 2020.11.7

* [switch](https://blog.csdn.net/mengxin_xiaobai/article/details/103831063)

  ```c++
  switch中的continue和break区别:
  若switch外部没有循环，则break和continue没有区别。
  若switch外部还有循环，
  一. 若break,continue在switch外部，则二者作用的是外部循环。
  二. 若break,continue在switch内部，则break作用于switch，continue作用于外部循环。
  ```

* static_assert(sizeof(ct_packet_t) == 105,  //静态断言，在编译时就断言。
                "ct packet size mismatch.");

* 初始化一个结构体，里面的默认同类型的值是相等的，如int默认都为0，且可以比较

* strlen计算长度不包括结尾的\0,sizeof计算长度一直到第一个\0为止。

* 关于16进制数和8进制

  ```
  例如: \032 ： 0表示8进制，即8进制数32
  \xA5  :  x表示16进制，即表示16进制A5
  ```

* 静态函数能否为虚函数

     > 首先，从“宏观”上来说，static成员函数其实并不算“成员”，它相当于在类域中定义了一个全局函数（哈哈，好像有点儿自相矛盾，但是相信大家能够理解），所以static成员函数与对象是没有“耦合”关系的（即，可以直接通过类调用static成员函数）。但是，virtual成员函数是绝对的“成员”，它与对象是100%的“耦合”（即，只能通过对象来调用virtual成员函数才有意义）。 
     >
     > 其次，从“微观”上来说，为什么访问virtual成员函数一定要通过指针/引用/对象来进行呢（即，必须要有一个实际的对象存在）？因为要想正确定位到实际应该执行的函数，必须通过对象中的vptr（看清，是“对象中的vptr”，所以必须有对象）找到此class的virtual  table，然后利用virtual  table中某个索引处的函数指针来访问实际的成员函数。从此处可以看出，static成员函数的“不通过对象直接通过类名便可以调用”的特点不适用于virtual成员函数（virtual成员函数一定要通过指针/引用/对象来进行），所以函数不能同时为“virtual  static”。 
     >
     > 
     >
     > 
     >
     > 解释二：[http://topic.csdn.net/t/20060603/08/4797568.html  ](http://topic.csdn.net/t/20060603/08/4797568.html)（CSDN [liking100](http://hi.csdn.net/liking100)）
     >
     > static成员没有this指针是关键！ 
     > static  function都是静态决议的（编译的时候就绑定了）， 
     > 而virtual  function  缺是动态决议的（运行时候才绑定）！ 
     > 所以virtual  function  不能为static！

* 若在基类和子类中都使用单例模式，基类和子类构造时都会调用各自的单例函数，并不是基类的函数就直接成了子类的函数，在调用distance时仍然会优先调用基类的单例函数，若要使用多个单例时，只能重新定义一个类，并将我们定义的上一个类更名

* 小端模式下截取二进制的位时，例如

     ```c++
     struct structA{
         uint16_t a:1 ;
         uint16_t b:15 ;
     }__attribute__((packed));
     uint16_t c = 0xa5;
     structA * a = (structA*)&c;
     // a 为1， b为 82
     ** 所以可以证明小端模式下取具体位是从字节的最低位开始的，0xa5 的二进制为10100101 00000000,a的二进制位 0x01, b的二进制位 1010010 00000000**
     ```

     

* [静态变量和全局变量的区别在于全局变量对所有的函数都是可见的，而静态局部变量只对定义自己的函数体始终可见。]()https://blog.csdn.net/weibo1230123/article/details/77917736

* 模板类的继承

     ```c++
     template <class T>
     class SearchArray:public FreeArray<T>  ///> FreeArray<T>
     {
     public:
         //构造函数
         SearchArray(int s):FreeArray<T>(s){}
         //拷贝构造函数
         SearchArray(const SearchArray &);
         //查找特定元素
         int findItem(T);
     };
     
     ```

     