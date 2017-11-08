传感器打开和关闭

```cpp
IKinectSensor::Open(); 
IKinectSensor::Close();
```





轮询模式 更适合游戏

```cpp
IKinectSensor::get_ColorFrameSource(IColorFrameSource**);
//获取一个ColorFrameSource (彩色帧源)
IColorFrameSource::OpenReader(IColorFrameReader**);
//打开一个ColorFrameReader(彩色帧读取器)
IColorFrameReader::AcquireLatestFrame(IColorFrame**);
//获取彩色帧，有就返回S_OK 
```

事件模式 更适合一般程序
`Windows`下使用WaitForMultipleObjects、WaitForMultipleObjects用于线程同步

```cpp
IKinectSensor get_ColorFrameSource(IColorFrameSource**);
```



