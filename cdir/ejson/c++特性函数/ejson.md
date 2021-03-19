* assert

  ```
  assert宏的原型定义在<assert.h>中，其作用是如果它的条件返回错误，则终止程序执行
  ```

* 定义宏函数

  ```
  #define CHECKTYPE(a)  \
     if(a == 0x01){}
  ```

* c++ 宏

  ```
  __VA_ARGS__ : 可变参数宏，即最后一个参数为省略号
  ##__VA_ARGS__ 宏前面加上##的作用在于，当可变参数的个数为0时，这里的##起到把前面多余的","去掉的作用,否则会编译出错
  
  #define my_print2(fmt,...)  printf(fmt,__VA_ARGS__)  
  my_print2("iiiiiii\n")       编译失败打印，因为扩展出来只有一个参数，至少要两个及以上参数
  
  #define my_print2(fmt,...)  printf(fmt,##__VA_ARGS__)  
  ```

* initializer_list

  ```
  initializer_list是某种类型的数组，但是内部数据都是const T类型，可以整体作为参数传递，由{}进行初始化。
  
  initializer_list对象只能用大括号{}初始化。
  
  拷贝一个initializer_list对象并不会拷贝里面的元素。其实只是引用而已。而且里面的元素全部都是const的。
  
  ///> 在c++11之前，max函数的源程序是这样的,只能比较两者之间的大小
  template <class T> const T& max (const T& a, const T& b);
  template <class T, class Compare>
    const T& max (const T& a, const T& b, Compare comp);  //支持自己编写的比较函数
    
  ///>但是有了initializer_list后，c++11标准库中添加另外一种实现方式max函数可以传递更多的参数
  template <class T> T max (initializer_list<T> il);
  template <class T, class Compare>
    T max (initializer_list<T> il, Compare comp);
    
  ///>例子
  cout << max({ 54,16,48,5 }) << endl;
  ```

* 定义枚举量的同时定义一个枚举变量（即对象），可以全局使用。

  ```
  enum JSONType {
              UNKNOWN,
              ARRAY,
              OBJECT,
          } type = UNKNOWN;  //定义一个type对象。
  ```

* 移动构造函数

  ```
  移动构造函数是浅拷贝，std::move,拷贝构造函数是深拷贝
  vector中,push_back()需要先创建一个临时对象，然后用拷贝构造函数添加进去，在进行释放，
  emplace_back 直接调用构造函数，不需要调用拷贝构造函数。
  ```

  

