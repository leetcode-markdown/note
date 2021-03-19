# qserialport qt 串口在子线程发送没有响应，失败

-  3YL
-  2021-02-24 11:11:29
-  [VC++/QT桌面编程](http://labisart.com/blog/index.php/Home/Index/category/cid/33)
-  23

如果串口在gui线程，收发一点问题都没有。如果放到子线程，就会发现发送不出去，代码：

```
    ``dbuffer[idx++] = 0x40;  ``// 起始标识符``    ``dbuffer[idx++] = 5;    ``// 长度``    ``dbuffer[idx++] = 1;    ``// 设备号``    ``dbuffer[idx++] = 0;    ``// 设备id``    ``dbuffer[idx++] = 0x1A;  ``// 亮度设置``    ``dbuffer[idx++] = lightData->chId;  ``// 通道号``    ``dbuffer[idx++] = lightData->val&0xFF;``// 亮度设置` `    ``// 校验和，前面的全部相加``    ``uint8_t sum = 0;` `    ``for``(``int` `i=0;i<7;i++)``      ``sum += dbuffer[i];` `    ``dbuffer[idx++] = sum;` `    ``QString hex = QtUtility::debugHex((``char``*)dbuffer,8);``    ``qint64 dw = ctrl->serial.hwPort->write((``const` `char``*)dbuffer,8);
```

找半天，总算知道原因了：

在write之后，必须要等待写出去完毕才执行下一步，否则线程跑到别的地方进行休眠就会把数据缓存到iodevice中：

加上这句就好了：

```
ctrl->serial.hwPort->waitForBytesWritten();
```