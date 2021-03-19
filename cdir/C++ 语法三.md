# C++ 语法三

* **sizeof** 和 **strlen**

  > strlen 用来就算字符串的长度，到第一个'\0'结束，且不包括结束字符。
  >
  > sizeof 针对 char * 类型时，总会返回字符串的长度，而不会向char a[5] 那样返回数组的长度。

* new  释放的问题

  **new 申请的空间不会被自动释放**

  ```c++
  #include <iostream>
  #include <string>
  #include <stdlib.h>
  #include <stdio.h>
  #include <string.h>
  using namespace std;
  
  //返回的a的值（即具体的地址值），返回值会拷贝，所以不为空
  char * test1(){
    char *a = new char[10];
    memcpy(a,"aass",4);
    return a;
  }
  
  //传入的是a 的值（地址），因为是形参，且不是引用或者二级指针，因此形参的值并没有改变
  void test2(char *a){
      a = new char[10];
      memcpy(a,"aass",4);
      cout << "a:" << a << endl;
  }
  
  int main()
  {
  //  char * b = test1();
  //  cout << "b:" << b << endl;
      char  b[] = "abc";
      test2(b);
      cout << "b:" << b << endl;
      return 0;
  }
  
  
  ```

* fmod

  ```
  fmod(a,b); //代表a 除以b的余数
  ```

  
