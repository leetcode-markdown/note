# TEA

### 1.使能

> 使能是开信号质量，失能是关信号质量，使能的包点数为507，
>
> 失能的信号点数为1014.

## 2.数据包结构体

 

```c++
typedef struct
{
 uint16_t frame_head; //包头 0xffee
 uint16_t sacn_frequency; //扫描频率
 uint16_t health;  //健康信息
 uint16_t point_num;  //点数
 uint16_t start_angle; //起始角
 uint16_t stop_angle; //结束角
 uint64_t time_stamp; //时间戳
 Point_Type point[POINT_NUM];//点云
} Data_Frame_Type;
```

