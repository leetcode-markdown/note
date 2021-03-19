

# c++ 语法一

*2020.10.26~2020.11.2* 

------------------------------------------------------------------------------------------------

------

## 2020.10.26

* c++ 预处理

  ```c++
  #if  defined(_MSC_VER)  //判断宏是否定义
  #pragma  comment(lib,"xxx.lib") //链接一个文件，本文中为静态库
  ```

* c++ double 、int

  ```c++
  double  s = (t >> 1) /64;  //t必须为int型，s的结果也为整数，只是最后将整数的类型转换下
  ```

* c++ 异或运算，位相同则为0，不同则为1

  ```
  1010 与 1100 异或的结果为0110
  ```


## 2020.10.27

* cmake 语法

  | cmake_minimum_required（）                            | VERSION后面加版本号                                          | 表示所需最小版本                                             |
  | ----------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | project()                                             | LANGUAGE 加  C  CXX                                          | 表示需要的编程语言，LANGUAGE可省略                           |
  | set(ASC  1)                                           | set里面分别为变量和值                                        | 给变量赋值，包括宏变量                                       |
  | IF(A  EQUAL  8)    ELSE()    ENDIF()                  | 判断条件                                                     | IF里面为条件，后面可接set语句                                |
  | set(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS}  -std=c++11" | 是c++的编译选项                                              | 代表加入c++11支持，类似的语句有add_compile_options           |
  | add_compile_options(-fPIC)                            | 增加编译选项                                                 | -fPIC代表产生与位置无关的代码，及产生的都是相对位置，代表可以在任何地方执行，动态库必备。 |
  | add_definitions(-DDEBUG)                              | 增加编译选项，也可以增加预处理定义                           | 例如，add_definitions(-DDEBUG)，和add_compile_options基本相同 |
  | file(glob Sources *.cpp)                              | 将所有的.cpp存到Sources中                                    |                                                              |
  | add_executable(Cars $(Sources) $(Includes))           | 用所有.cpp，.h文件编译成名为Cars的可执行文件                 |                                                              |
  | include_directories(${PROJECT_SOURCE_NAME}/include)   | 指定包含头文件的目录                                         |                                                              |
  | link_libraries("")                                    | 添加要链接的库文件路径                                       |                                                              |
  | add_definitions("-DONNX_NAMESPACE=${ONNX_NAMESPACE}") | 在源文件的编译中添加-D define标志。                          |                                                              |
  | add_subdirectory(third_party/onnx EXCLUDE_FROM_ALL)   | 新添加一个目录位置，编译这个目录中所有的内容，一般这个目录中也会包含CMakeLists文件 |                                                              |
  | find_package(OpenCV REQUIRED)                         | 这个命令是cmake中经常使用的命令，如果我们想在cmake中使用一些其他的大型开源项目(编译好的)，例如OpenCV，在我们将OpenCV编译好之后，如果我们想使用它，我们就可以在cmake中添加。 |                                                              |
  | list(append GPU_ARCHS  51 61 75)                      | 往GPU_ARCHS里面添加51，61，75变量                            |                                                              |
  | config.cmake                                          | 如果需要我们的CMakeLists有一定的自由配置，比如，我们需要开启CUDA的支持，或者关闭某个功能。如果功能项比较多的话，每次增加功能或者修改，直接在CMakeLists中写一堆代码命令会很麻烦。在这种情况下的话，最好是另外创建一个名为`config.cmake`的文件，这个文件中填写了我们的配置信息(举个例子)： |                                                              |
  | include(install_package)                              | 引入install_package.cmake模块,设置CMAKE_MODULE_PATH可以改变他的当前目录 |                                                              |
  | if(COMMAND cmake_policy)                              | 检查cmake_policy函数或宏是否被定义                           |                                                              |
  | if(DEFINED address)                                   | 检查是否定义address这个变量                                  |                                                              |
  | option(BUILD_TEST  "Build  test"  ON)                 | 设置cmake编译时链接命令选项，默认为ON                        |                                                              |
  
  


* cmake判断平台
  
  ```cmake
  if(WIN32 AND NOT MINGW)
        message("WIN32 编译设置")
     elseif(WIN32 AND MINGW)
       message("MINGW 编译设置")
     elseif(UNIX AND NOT ANDROID)
       message("UNIX 编译设置")
     elseif(ANDROID)
      message("ANDROID 编译设置")
     endif()
     
    //： CMAKE_SIZEOF_VOID_P # 为4 代表32位平台，为8 代表64为平台
  ```
  
* cmake 宏

  > CMAKE_C_COMPILER：指定C编译器
  > CMAKE_CXX_COMPILER：指定C++编译器
  >
  > CMAKE_SIZEOF_VOID_P:  为4 代表32位平台，为8 代表64为平台
  >
  > CMAKE_POSITION_INDEPENDENT_CODE: 为 ON 代表产生与位置无关的代码，OFF关闭
  >
  > PROJECT_SOURCE_DIR ：当前项目的路径
  >
  > PROJECT_BINARY_DIR ：项目编译后存放的路径
  >
  > CMAKE_CURRENT_BINARY_DIR ：与PROJECT_BINARY_DIR基本相同
  >
  > CMAKE_CURRENT_SOURCE_DIR ：与PROJECT_SOURCE_DIR基本相同
  >
  > CMAKE_MODULE_PATH: 用于指定要由CMake加载的CMake模块的搜索路径[`include()`](https://cmake.org/cmake/help/v3.5/command/include.html#command:include) 或者 [`find_package()`](https://cmake.org/cmake/help/v3.5/command/find_package.html#command:find_package)命令，然后检查CMake随附的默认模块。默认情况下，它是空的，打算由项目设置。
  >
  > CMAKE_EXPORT_COMPILE_COMMANDS: 在生成期间启用/禁用编译命令的输出。如果启用，将生成一个compile_commands.json文件，其中包含m中项目所有翻译单元的确切编译器调用。

* c++ 库函数。
  
  * explict可以避免不合时宜的类型转换，CxString  string1(24);和CxString string2 = 10;都可以，是因为当类的构造函数只有一个参数时，编译时会有一个缺省的转换操作，将构造函数对应类型的数据转换成该类的对象。
  * ProperityBuilderByName(type , name , protected) 用来创建一个变量的方法，会生成变量名m_Name,,setName和getName来对其进行修改。
  * 1秒等于1000毫秒，1毫秒等于1000微秒，usleep函数的单位是微秒。
  
* cmake连接大型开源项目

  ```
  find_package(OpenCV REQUIRED)
  
  message(STATUS "OpenCV library status:")
  message(STATUS "    version: ${OpenCV_VERSION}")
  message(STATUS "    libraries: ${OpenCV_LIBS}")
  message(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}")
  
  add_executable(example main.cpp)
  target_link_libraries(example ${OpenCV_LIBS})
  ```

* cmake 用循环设置变量

  ```
  list(APPEND GPU_ARCHS
      51
      61
      75
      )
  
  foreach(arch ${GPU_ARCHS})
      set(GENCODES "${GENCODES} -gencode arch=compute_${arch},code=sm_${arch}")
  endforeach()
  
  ```

  

## 2020.10.28

* c++ 中NULL 和 nullptr的区别

  ```
  void  func(void *t){
   cout << "func1" <<endl;
  }
  void  func(int i){
    cout << "func2" << endl;
  }
  int main (){
    func(NULL);
    func(nullptr);
    return  0;
  }
  ```

  // 结果输出为：func2

  ​                         func1

  **看起来都表示空指针，NULL却在重载函数的时候匹配到了参数为int的那个版本，在c++ 中NULL表示着0，void* 类型不允许隐式转换成其他类型，所以加入了nullptr,表示在任何情况下都表示为空指针**

* 取类型的最大值和最小值

  ```
  std::numeric_limits<uint32_t>::max();
  std::numeric_limits<uint32_t>::min();
  ```

* 创建锁

  ```
  pthread_mutex_init(pthread_mutex_t *,NULL); //第二个参数指定了锁的属性，为NULL则使用默认属性
  ```

* 调用c++ 库函数

  ```
  调用c++自带的库函数时，若库函数和本地的函数重名，则前面加上::表示调用c库函数,例如 ::memset
  ```

* 终端控制(getTermios)

  [cfmakeraw](https://blog.csdn.net/williamwang2013/article/details/8560552)    [串口termios函数](https://blog.csdn.net/williamwang2013/article/details/8560552)

  ```
  * tcgetattr 用来获取终端参数
  * ioctl是设备驱动程序中对设备的I/O通道进行管理的函数。所谓对I/O通道进行管理，就是对设备的一些特性进行控制，例如串口的传输波特率、马达的转速等等。它的调用个数如下：int ioctl(int fd, ind cmd, …)
  * tcflush Unix终端I/O函数，包含头文件 #include <termoios.h>,分别有下面3种类型，
  TCIFLUSH   //清除正收到的数据，不会读取出来
  TCOFLUSH   //清除正写入的数据，且不会发送至终端
  TCIOFLUSH  //清除所有正在发生的I/O数据。
  * cfmakeraw： Raw模式可以禁止行缓冲(line buffering)，处理挂起（CTRLZ）、中断或退出（CTRLC）等控制字符时，将直接传送给程序去处理而不产生终端信号，而cfmakeraw就是设置Raw模式的
  * int   tcdrain (int fd);    //等待所有写入fd中的数据输出
  ```

* 波特率、比特率、采样率、数据传输率

  [采样率](https://blog.csdn.net/q1281405619/article/details/108253494)

  ----

  ### 比特率

  比特率(bit rate)又称传信率、信息传输速率(简称信息速率，information rate)。其定义是：通信线路(或系统)单位时间(每秒)内传输的信息量，即每秒能传输的二进制位数，通常用Rb表示，其单位是比特/秒(bit/s或b/s，英文缩略语为bps)。

  ---

  ### 波特率

  波特率(Baud rate)又称传码率、码元传输速率(简称码元速率)、信号传输速率(简称信号速率，signaling rate)或调制速率。其定义是：通信线路(或系统)单位时间(每秒)内传输的**码元(脉冲)**个数；或者表示信号调制过程中，单位时间内调制信号波形的变换次数，通常用RB表示，单位是波特(Bd或Baud，前者规范)。

  ---

  ### 数据传输率

  数据传输率(data transfer rate)又称数据传输速率、数据传送率。其定义是：通信线路(或系统)单位时间(每秒)内传输的字符个数；或者单位时间(每秒)内传输的码组(字块)数或比特数。其单位是字符/秒；或者码组/秒、比特/秒(可见，当数据传输率用“bit/s”作单位时，即等于比特率)。 **所以它的单位在不同的应用中是不同的。**

  ---

  ### 采样率

  采样频率,也称为采样速度或者采样率,定义了每秒从连续信号中提取并组成离散信号的采样个数,它用赫兹(Hz)来表示。

  ---

  

*  **pthread_cond_signal**

  pthread_cond_signal函数的作用是发送一个信号给另外一个正在处于阻塞等待状态的线程,使其脱离阻塞状态,继续执行.如果没有线程处在阻塞等待状态.

* **reinterpret_cast<new_type> (expression)**

  reinterpret_cast运算符是用来处理无关类型之间的转换；它会产生一个新的值，这个值会有与原始参数（expression）有完全相同的比特位。

* c语言宏，FD_ISSET 、FD_SET、 FD_ZERO

  [C++ select() 多路复用](https://blog.csdn.net/qq_39871498/article/details/90733415)

   
  
  ```
  FD_ISSET(int fd,fd_set *fdset); //判断fd是否在给定的描述符集中，通常配合select使用，若在则返回非零值，否则返回零。
  FD_SET(fd，&set); //将fd加入set集合
  FD_ZERO(&set); //将set清零使集合中不含任何fd*
  
  函数原型：
  int select(int maxfd,fd_set *rdset,fd_set *wrset, \  
             fd_set *exset,struct timeval *timeout);  
  参数说明：
  参数maxfd是需要监视的最大的文件描述符值+1；rdset,wrset,exset分别对应于需要检测的可读文件描述符的集合，可写文件描述符的集 合及异常文件描述符的集合。struct timeval结构用于描述一段时间长度，如果在这个时间内，需要监视的描述符没有事件发生则函数返回，返回值为0。
  ```




## 2020.10.29

* linux锁管理

  ```
  pthread_mutex_trylock:函数pthread_mutex_trylock是pthread_mutex_lock的非阻塞版本。如果mutex参数所指定的互斥锁已经被锁定的话，调用pthread_mutex_trylock函数不会阻塞当前线程，而是立即返回一个值来描述互斥锁的状况
  pthread_mutex_timedlock: 和pthread_mutex_trylock 基本相似，他代表在到达超时时间时，若还未获得锁，将返回一个非零的错误码。
  
  ```

* linux条件变量

  ```
  pthread_cond_init(&cond, NULL); /* 动态初始化条件变量 */
  pthread_cond_t cond = PTHREAD_COND_INITIALIZER; /* 静态初始化条件变量 */
  pthread_cond_wait(&cond); /* 等待条件变量触发，使用wait之前，必须要上锁，因为函数里面会进行解锁。*/
  pthread_cond_timedwait(&cond); /* 超时等待条件变量触发 ，当在指定时间内有信号传过来时，返回0，否则返回一个非0数（我没有找到返回值的定义);*/
  pthread_cond_signal(&cond); /* 激活一个等待该条件的线程，单播 */
  pthread_cond_broadcast(&cond); /* 激活所有等待该条件的线程，广播 ，而对于pthread_cond_broadcast函数，它使所有由参数cond指向的条件变量阻塞的线程退出阻塞状态，如果没有阻塞线程，则函数无效*/
  pthread_cond_destroy(&cond); /* 销毁条件变量 ,调用destroy函数解除条件变量并不会释放存储条件变量的内存空间,静态创建的条件变量不能调用这个函数*/
  
  条件变量属性（pthread_condattr_t）:
  注：时钟属性控制计算pthread_cond_timewait函数的超时参数（tsptr）时采用的是哪个时钟
  pthread_condattr_init函数：
  功能：对条件变量属性结构体初始化
  调用此函数之后，条件变量属性结构体的属性都是系统默认值，如果想要设置其他属性，还需要调用不同的函数进行设置
  pthread_condattr_destroy函数：
  功能：对条件变量属性结构体反初始化（销毁）
  只反初始化，不释放内存。
  pthread_condattr_setshared函数：
  功能：设置条件变量的进程共享属性
  pthread_condattr_getshared函数：
  功能：获取条件变量的进程共享属性
  pthread_condattr_setclock函数：
  功能：此函数用于设置pthread_cond_timewait函数使用的时钟ID
  pthread_condattr_getclock函数：
  功能：此函数获取可被用于pthread_cond_timedwait函数的时钟ID。pthread_cond_timedwait函数使用前需要用pthread_condattr_t对条件变量进行初始化
  
  ```

  示例1：[链接](https://blog.csdn.net/techhome803/article/details/8276058)

  ```
  
  #include <stdio.h>
  #include <unistd.h>
  #include <stdlib.h>
  #include <string.h>
  #include <pthread.h>
  
  pthread_mutex_t lock;
  pthread_cond_t cond;
  
  void *thread_1(void *data)
  {
      pthread_mutex_lock(&lock);
      pthread_cond_wait(&cond, &lock);
      printf("%s\n", __func__);
      pthread_mutex_unlock(&lock);
  }
  
  void *thread_2(void *data)
  {
      pthread_mutex_lock(&lock);
      printf("%s\n", __func__);
      pthread_mutex_unlock(&lock);
  
      pthread_cond_signal(&cond);
  }
  
  int main(int argc, char const *argv[])
  {
      pthread_t pid[2];
      pthread_mutex_init(&lock, NULL);
      pthread_cond_init(&cond, NULL); 
  
      pthread_create(&pid[0], NULL, thread_1, NULL);
      pthread_create(&pid[1], NULL, thread_2, NULL);
  
      pthread_join(pid[0], NULL);
      pthread_join(pid[1], NULL);
  
      pthread_mutex_unlock(&lock);
      pthread_mutex_destroy(&lock);
      pthread_cond_destroy(&cond);
  
      return 0;
  }
  ```

  <!--**条件变量始终都会和一个互斥锁配合使用，当pthread_cond_wait()被调用阻塞住线程的时候，lock会被自动释放，当信号来的时候会自动上锁。thread_1获取到互斥锁之后，因为条件变量的存在，thread_1被阻塞住，互斥锁自动释放掉，当条件变量满足条件之后系统会将互斥锁再重新锁上**-->



* 宏定义

  * #ifdef...#else...#endif: 如果定义了某个宏，则运行#else之前的内容
  * #ifndef...#else...#endif:如果没有定义宏，则运行#else之前的内容
  * #if...#else...#endif:如果某个条件为真，为真即不为0，则运行#else之前的内容。
  * enum Name {WQE,ASD}：声明一个NAME类型，有两个值，WQE默认为1.
  * typedef  long  time_t   : 将long类型命名成别名time_t.
  * #define   __S32_TYPE  int: 代表将int 类型命名为 \__S32_TYPE ,和typedef顺序相反，typedef是要命名的类型在前，而#define是要命名的类型在后。 
  
* 基础类型
  
  ```
  _time_t: typedef long     time_t;    /* 时间值time_t 为长整型的别名*/
  __syscall_slong_t : //表示纳秒
  时间单位: 1s = 10^3 ms = 10^6 微秒 = 10^9 纳秒 
  fd_set :
  ```
  

  
* 类型长度

  | C 数据类型      | LP32 | LP64 |
  | --------------- | ---- | ---- |
  | `char`          | 8    | 8    |
  | `short`         | 16   | 16   |
  | `int`           | 32   | 32   |
  | `long`          | 32   | 64   |
  | `long` `long`   | 64   | 64   |
  | `pointer`       | 32   | 64   |
  | `enum`          | 32   | 32   |
  | `float`         | 32   | 32   |
  | `long` `double` | 128  | 128  |

* assert（?）:当assert里面的函数条件为假时，终止程序的运行。

* 系统时间设置及获取

  ```
  timeval 和 timespec 用来获取更高精度的时间。
  int  clock_gettime(clockid_t,struct timespec *)用来获取特定时钟的时间。
  时钟类型如下：
  CLOCK_REALTIME 统当前时间，从1970年1.1日算起
  CLOCK_MONOTONIC 系统的启动时间，不能被设置
  CLOCK_PROCESS_CPUTIME_ID 本进程运行时间
  CLOCK_THREAD_CPUTIME_ID 本线程运行时间
  
  #include<sys/time.h>
  int gettimeofday(struct  timeval*tv,struct  timezone *tz )
  用来获取当前的时间，类似于上述的CLOCK_REALTIME.
  ```

* 线程安全理解

  ```
  线程安全就是多线程访问时，采用了加锁机制，当一个线程访问该类的某个数据时，进行保护，其他线程不能进行访问直到该线程读取完，其他线程才可使用。不会出现数据不一致或者数据污染。
  线程不安全就是不提供数据访问保护，有可能出现多个线程先后更改数据造成所得到的数据是脏数据
  ```

* 函数参数修饰符

  + restrict，C语言中的一种类型[限定符](https://baike.baidu.com/item/限定符/1924249)（Type Qualifiers），用于告诉编译器，对象已经被指针所引用，不能通过除该指针外所有其他直接或间接的方式修改该对象的内容。
  +   __attribute__((packed)) ，取消结构体对齐，类似于#pragma  pack(1)

* Signal()信号处理函数

  ```
  #include <signal.h>
  typedef void (*sighandler_t)(int);
  sighandler_t signal(int signum, sighandler_t handler);
  第一个参数signum：指明了所要处理的信号类型，它可以取除了SIGKILL和SIGSTOP外的任何一种信号。 　
  第二个参数handler：描述了与信号关联的动作，它可以取以下三种值：
   （1）SIG_IGN：表示忽略该信号
    (2) SIG_DFL：表示按默认执行
    (3) sighandler_t类型的函数指针：表示接收到信号后，按函数里面的方法执行。
  ```

* 纯虚函数必须要在子类中实现才可以调用，因为在基类中只有声明而没有定义，虚函数可以直接使用。

  > 虚函数的定义形式： virtual {method body};
  >
  > 纯虚函数的定义形式:   virtual { } =  0;

* c Math 

  | 函数名 | 用法      | 描述        |
  | ------ | --------- | ----------- |
  | fmod   | fmod(a,b) | 求a/b的余数 |
  |        |           |             |

* 友元类，friend class CC;即CC可以访问当前类的所有成员。

* hostent是host entry的缩写，该结构记录[主机](https://baike.baidu.com/item/主机/455151)的信息，包括[主机名](https://baike.baidu.com/item/主机名/2836107)、别名、地址类型、地址长度和地址列表。之所以主机的地址是一个列表的形式，原因是当一个主机有多个网络接口时，自然有多个地址。

* 结构体对齐：

  ```
  请牢记以下3条原则：（在没有#pragma pack宏的情况下）
  
  1、数据成员对齐规则：结构体（struct）的数据成员，第一个数据成员放在offset为0的地方，之后的每个数据成员存储的起始位置要从该成员大小的整数倍开始（比如int在32位机子上为4字节，所以要从4的整数倍地址开始存储）。
  
  2、结构体作为成员：如果一个结构体里同时包含结构体成员，则结构体成员要从其内部最大元素大小的整数倍地址开始存储（如struct a里有struct b,b里有char,int ,double等元素，那么b应该从8(即double类型的大小)的整数倍开始存储）。
  
  3、结构体的总大小：即sizeof的结果。在按之前的对齐原则计算出来的大小的基础上，必须还得是其内部最大成员的整数倍，不足的要补齐（如struct里最大为double，现在计算得到的已经是11，则总大小为16）。
  ```

  ```
  当在结构体 中包含 共用体 时，共用体在结构体里的对齐地址为共用体本身内部所对齐位数，如下：
  typedef union{
  	long i;
  	int k[5];
  	char c;
  }DATE;
  struct data{
  	int cat;
  	char cc;
  	DATE cow;
  	char a[6];
  };
  sizeof(DATE)=20, 而在结构体中中是4+1+3（补齐4对齐）+20+6+2（补齐4对齐）=36；
  ```

* 信号处理：

  [信号](https://baike.baidu.com/item/sigaction/4515754?fr=aladdin)，[信号样例](https://blog.csdn.net/weibo1230123/article/details/81411827)

  ```
  sigaction: 用来查询和设置信号处理方式。
  int sigaction(int signum, const struct sigaction *act,
                       struct sigaction *oldact);
  /*
  *signum参数指出要捕获的信号类型，act参数指定新的信号处理方式，oldact参数输出先前信号的处理方式（如果不为*NULL的话）,oldact只是做了个备份而已。
  */
  sigemptyset: 用法int sigemptyset(sigset_t *set); ,用来将set信号集初始化并清空。
  
  ```

* union联合体

  ```
  union 名称{
  	public: //此行可不写，默认为public
  		公有成员
  	protected:
  		保护型成员
  	private:
  		私有成员
  };
  ```

  <!--union 也可以省略名称，则为无名结构体，可以直接调用其成员函数-->

* 内联函数，是将函数替换成代码，而不用申请调用函数所需要调用的空间，类中，只要是在类中定义的都叫内联函数，无论其是否定义，内联函数必须要在函数定义前加关键字inline,而不是声明处。

* strerror()用来依参数errnum 的错误代码来查询其错误原因的描述字符串, 然后将该字符串指针返回.

  
## 2020.10.30


* c++ 域作用符

  > 1.用于区分全局变量和局部变量，变量名前加上:: 就表示全局变量。
  >
  > 2.成员函数定义。
  >
  > 3.名空间作用域

* 迭代器

  [迭代器](https://blog.csdn.net/cnd2449294059/article/details/72782099)

  ```
  vector<int> vv(10,9);  
  const vector<int> :: iterator iter = vv.begin();
  当const 在前时， iter不可改变，指向的值可以改变，所以++iter;是错误的写法
  
  vector<int> vv(10,9);  
  vector<int> :: const_iterator iter;  
  当为const_iterator 时，可以增加，指向的值不能改变。
  ```

* 文件信息获取（glob）

  ```
  glob库函数用于Linux文件系统中路径名称的模式匹配，即查找文件系统中指定模式的路径。注意，这不是正则表达式匹配，虽然有些相似，但还是有点差别。
  
  glob函数原型
  #include <glob.h>
  int glob(const char *pattern, int flags,
                          int errfunc(const char *epath, int eerrno),glob_t *pglob);
                          
  glob_t使用完后，要配合globfree进行释放。    
  glob函数搜索匹配 函数pattern中的参数，如/*是匹配根文件下的所有文件（不包括隐藏文件，要找的隐藏文件需要从新匹配），然后会将匹配出的结果存放到 pglob，即第4个参数中，第二个参数能选择匹配模式，如是否排序，或者在函数第二次调用时，是否将匹配的内容追加到pglob中，等，第3个参数是查看错误信息用，一般置为NULL；
  ```

* c++ 函数携带可变参数

  [可变参数](https://www.cnblogs.com/betterwgo/p/10623513.html)    [vsnprinf](https://blog.csdn.net/leiwangzhongde/article/details/83029220)

  

  > 1.函数声明用省略号（...）代替可变参数，编译器不对后面的参数进行参数检查，需配合va_start ,va_arg,va_end来对可变参数进行处理。
  >
  > 2.可变参数可以配合vsnprintf来组合字符串.
  >
  > 3. realloc 类似于 vector的resize，即手动扩大堆空间。
  
* 文件操作

  | 函数名   | 用法                                 | 备注                              |
  | -------- | ------------------------------------ | --------------------------------- |
  | realpath | realpath(char *,NULL)                | 求绝对路径                        |
  | compare  | compare(int a,int b,string str)      | 从下标a开始和str比较b位           |
  | string   | std::string(string str,int a, int b) | 复制a到b位的字符串，类似于 substr |
  | stat     | stat(char *,struct stat *)           | 判断文件是否存在                  |
  | getline  | getline(ifstream *,string)           | 从流中读取数据放到string中        |

  

* fstream头文件

  [ifstream](https://blog.csdn.net/sinat_36219858/article/details/80369255)

  ```
  fstream头文件定义了三种支持文件IO的类型：
  　　*istringstream从文件中读取；由istream派生而来*
  　　*ostringstream写到文件中去；由ostream派生而来*
  　　*fstream读写文件；由iostream派生而来*
  　　*ofstream是从内存到硬盘，ifstream是从硬盘到内存，其实所谓的流缓冲就是内存空间*
  　　*输出模式则是输出到文件，输入默认则是输入到内存（如从键盘输入一个数）*
  　　*iostream 处理控制台 IO*
      *fstream 处理命名文件 IO*
      *stringstream 完成内存 string 的IO*
  ```

* volatile的使用

  ```
  static  volatile  sig_atomic_t  g_signal_status = 0; //volatile代表每次取这个值时都要小心论证。
  ```

* 嵌套类（class A::B）

   在一个类的内部定义另一个类，我们称之为嵌套类（nested class），或者嵌套类型。之所以引入这样一个嵌套类，往往是因为外围类需要使用嵌套类对象作为底层实现，并且该嵌套类只用于外围类的实现，且同时可以对用户隐藏该底层实现。

    虽然嵌套类在外围类内部定义，但它是一个独立的类，基本上与外围类不相关。它的成员不属于外围类，同样，外围类的成员也不属于该嵌套类。嵌套类的出现只是告诉外围类有一个这样的类型成员供外围类使用。并且，外围类对嵌套类成员的访问没有任何特权，嵌套类对外围类成员的访问也同样如此，它们都遵循普通类所具有的标号访问控制。

* [fcntl](https://blog.csdn.net/xingzhi2014/article/details/14025855)

  根据文件描述词来操作文件的特性,即对read 和 write 这个函数进行底层修改。

* 类型转换

  | 名称             | note                                                         | 用法                                                         |
  | ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | const_cast       | 去掉类型的const或volatile属性                                |                                                              |
  | static_cast      | 无条件转换，静态类型转换                                     | 基本数据类型转换，enum，struct，int，char，float等。static_cast不能进行无关类型（如非基类和子类）指针之间的转换。 |
  | dynamic_cast     | 有条件转换，动态类型转换，运行时检查类型安全（转换失败返回NULL） | 安全的基类和子类之间的转换。必须有虚函数。相同基类不同子类之间的交叉转换，但结果返回NULL。 |
  | reinterpret_cast | 仅重新解释类型，但没有进行二进制的转换                       | 最普通的用途就是在函数指针类型之间进行转换，在比特级别上进行转换，可以把一个指针转换成一个整数 |

* x86下windows和fedora都是小端

