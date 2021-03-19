# CYLidar.cpp

* **doProcessSimple**

   ~~~c++
<sys_scan_time>:计算从等待到接收到信号并拷贝成功所消耗的时间。
<m_field_of_view>: 当前可见的视图的区域，第一次运行时为。
<ehco_angle>: 当前视图区域每个点的间隔角度.
<offsetSize>: 当前不可见视图区域的点数，其加上count为一圈的点数。 // echo_angle 和 offsetSize这两个值好像有问题。
<m_OffsetTime>: 未启用.
<m_PointTime>: TEA雷达情况下好像并未初始化。
<global_nodes[0].stamp>: 为当前串口缓冲区存在未扫描完毕的点，这些点的传输延迟，这样可以测出第一个点的真正时间。
    
   ~~~

* **checkLidarAbnormal**

  > while循环条件：当扫描的缓冲区小于10，且同时满足下面两个条件，其条件一为扫描时间为0.05或当前为双通道时，其条件二为op_result 为 RESULT_OK.
  >
  > ​	
  >
  > 