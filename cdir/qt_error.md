* multiple definition of 

​    **可能是pro文件中重复包含某一头文件，或源文件**



* ###### Qt_ 错误:cannot open output file debug\myWidget2.exe: Permission denied问题

   调试运行的时候遇到这个问题，发现是由于存在没有正常关闭的程序所致，所以我们只需要进入任务管理器-->进程-->找到project(自己创建工程的名字).exe，结束进程，然后重新调试运行便可以解决。