# OPENCV 学习

--by feng

## 快速上手

```c++
#include <opencv2/opencv.hpp>
using namespace cv;
void main()
{
  Mat srcImage = imread("pic.jpg");
  imshow("[source picture]",srcImage);
  return 0;
}
```

`imread`读图片

`imshow` 显示图片

```c++
//图像腐蚀
Mat srcImage = imread("pic.jpg");
imshow("腐蚀操作", srcImage);
Mat element = getStructuringElement(MORPH_RECT, Size(15, 15));
Mat dstImage;
erode(srcImage, dstImage, element);
imshow("效果图", dstImage);
```

```c++
//程序三 图像模糊
Mat srcImage = imread("pic.jpg");
imshow("wave0", srcImage);
Mat dstImage;
//均值滤波操作
blur(srcImage, dstImage, Size(8, 7));
imshow("wave1", dstImage);
```

```c++
//视频操作
VideoCapture capture;
capture.open("1.MTS");
while(1)
{
	Mat frame;
	capture >> frame;
	imshow("读取视频", frame);
	waitKey(30);
}
```

## Mat结构的使用

> 我们不必再手动的为其开辟空间，不必再不需要的时候立即将空间释放
>
> ```c++
> Mat A,C;//仅仅创建了信息头
> A = imread("1.jpg",CV_LOAD_IMAGE_COLOR);//为矩阵开辟内存
> Mat B(A);//使用拷贝构造函数
> C=A;//赋值运算符
> ///创建一个感兴趣的区域
> Mat D(A,Rect(10,10,100,100));//使用矩形界定
> Mat E = (Range:all(),Range(1,3));//用行和列界定
> ///克隆
> Mat F = A.clone();
> Mat G
> A.copyTo(G);
> ```
>

# 常用的数据结构

## 点的表示Point 类

```
Point point ;
point point.x=10;
point point.y=20;
//or
Point point(10,20);
```

## 颜色的表示Scalar类

```
Scalar(a,b,c)
c 红色
b 绿色
a 蓝色
```

## 尺寸的表示Size类

```
Size(width,height);
```

## 矩形的表示Rect类

```
Rect 
// 成员变量 x , y , width ,height
// 成员函数 area()面积 inside是否在矩形内 tl()左上角 br()右下角
Rect rect = rect1 & rect2; //并集
Rect rect = rect1 | rect2; //交集
Rect rectShift = rect + point;//平移
Rect rectScale = rect + Size;//缩放
```

## 其他常用知识点

* `Matx`是一个轻量级Mat，必须在使用前规定好大小Matx23f 2*3 float类型的`Matx`

* `Vec`是`Matx`的一个派生类，是一个一维的`Matx`，跟vector很相似

  ```
  template<typename_Tp,int n> class Vec:public Matx<_Tp, n, 1>{...};
  typedef Vec<uchar,2> Vec2b;
  ```

* Range类 为更像MATLAB产生的Range(a,b)

* 防止内存溢出的函数

* `<math.h>`里面一些函数使用起来很方便

#Core组件进阶

## 访问图像中的像素

图像矩阵的大小取决于所用的颜色模型，取决于所用的通道数
RGB图像中子列BGR顺序存储

## 颜色空间缩减

现有颜色空间值除以某个输入值，获取较少的颜色数
`Inew = (Iold/10)*10;`

```c++
//每次使用都会重新计算一次因此最好将每个像素进行一遍上述计算，也需要一定的时间花销，因为一共只有255种像素

int divideWith;
uchar table[256];
for(int i=0;i<256;i++)
	table[i] = divideWith * (i/divideWith);
/**
	因此table[i] 存放的是值为i的像素减少颜色空间的结果
	p[i] = table[p[i]];
*/
```

因此颜色空间缩减算法就可由下面两步组成

1. 遍历图像矩阵的每一个像素
2. 对像素应用上述公式

  ## LUT函数: Look up table

## 计时函数

`getTrickCount ` 返回CPU 某个事件以来走过的时钟周期数

`getTrickFrequency` 返回CPU 一秒钟走的时钟周期

```c++
double time0 = static_cast<double>(getTickCount());//记录其实时间
time0 = ((double)getTrickCount() - time0)/getTickFrequency();
cout<<time0<<" s"<<endl;
```

## 感兴趣的区域ROI

## 线性混合操作

$g(x) = (1 - a)f_{a}(x)+a{}f_{3}(x)$

### 计算数组的加权和

`addWeighted`

这个函数的作用是计算两个数组(图像矩阵)的加权和。原型如下

```c++
void addWeighed (InputArray src1,double alpha,InputArray src2,double beta,double gamma,OutputArray dst,int dtype=-1);
```

* 第一个参数 , `InputArray `src1表示需要加权的第一个数组,常常填一个`Mat`
* 第二个参数，double 类型的alpha ，表示第一个数组的权重
* 第三个参数，`InputArray`类型的src2表示第二个数组，他需要和第一个数组拥有相同的尺寸和通道数
* 第四个参数，double类型的beta，表示第二个数组的权重值
* 第五个参数，double类型的gamma，一个加到权重总和的标量值，其含义通过接下来列出的式子自然会理解
* 第六个参数，`OutputArray`类型的`dst`,输出的数组，他和输入的两个数组拥有相同的尺寸和通道数
* 第七个参数，`int`类型的`dtype`，输出矩阵的可选深度，默认为-1 等同于src1.depth()

# 分离颜色通道，多通道图像混合

## 通道分离

`split()`

函数原型 C++:

```c++
void split(const Mat &src,Mat* mvbegin);
void split(InputArray m ,OutputArray mv);
```

* 第一个参数 `InputArray`类型的的m或者Mat&类型的`src`我们需要的进行分离的多通道数组
* 第二个参数 `OutputArrayOfArrays`类型的mv填函数的输出数组或者输出的vector容器

`split`函数分割多通道数组转化成独立的单通道数组
公式 $mv[c](I) = src(I)_c$

## 通道合并

`merge()`

```c++
void merge(const Mat*mv,size_t count ,OutputArray dst);
void merge(InputArrayOfArrays mv,OutputArray dst);
```

* 第一个参数，mv 需要合并的输入矩阵或vector 容器的阵列，这个mv参数中所有的矩阵必须有一样的尺寸和深度
* 第二个参数，count。当mv为一个空白的C数组时，代表输入矩阵的个数，这个参数显然必须大于1
* 第三个参数，`dst`输出矩阵，和mv[0]拥有一样的尺寸和深度，并且通道的数量是矩阵阵列中的通道总数

# 图片对比度的亮度

## 理论依据

算子的概念，一般图像处理的算子都是一个函数，他接收一个或多个输入图像，并产生输出图像一般为以下形式

 $g(x)=h(f(x))$或者$g(x)=h(f_0(x)...f_n(x))$

亮度和对比度的操作属于图像处理变换中的一种--点操作。仅仅根据输入像素值来计算相应的输出像素值这类算子包括亮度、对比度调整，颜色校正和变换
两种最常见的点操作是乘上一个常数(对比度)以及加上一个常数(亮度)

$g(x) = a*f(x) + b$

# 离散傅里叶变换

​	离散傅里叶变换，是指傅里叶变换在时域和频域上都呈现离散的形式，将是与信号的采样变换为在离散时间傅里叶变换频域的采样，形式上，变换两端的序列是有限长的，而实际上着两组序列都应当被认为是离散周期信号的主值序列。即使对有限长的离散信号做DFT，也应当对其经过周期延拓成为周期信号再进行变换。实际应用中，通常采取快速傅里叶变换来高效计算DFT

# 图像处理

## 线性滤波:方框滤波，均值滤波，高斯滤波

###平滑处理

平滑处理也称为模糊处理，是一种简单且使用频率很高的图像处理方法，平滑处理的用途有很多，最常见的是用来减少图像上的噪声点或者失真，在设计及到降低图像分辨率时，平滑处理是非常好用的方法

###图像滤波与滤波器

​	图像滤波，是指在尽量保留图像细节特征的条件下对目标图像的噪声进行抑制，是图像预处理中不可缺少的操作，其处理效果的好坏将直接影响到后续图像处理和分析有效性和可靠性。

​	消除图像中的噪声成分叫做图像的平滑化或滤波操作。信号或图像的能量大部分集中在幅度谱的低频和中频段，而高频段，有用的信息经常被噪声淹没。因此一个能降低高频成分幅度的滤波器就能够减弱噪声的影响。

​	图像滤波的目的有两个:一个是抽出对象的特征作为图像识别的特征模式；另一个是为适应图像处理的要求，消除图像数字化时混入的噪声

###线性滤波: 方框滤波、均值滤波高斯滤波

线性滤波器:线性滤波器经常用于剔除输入信号中不想要的频率或者从许多频率中选择一个想要的频率

几种常见的线性滤波器如下

* 低通滤波器:允许低频率通过
* 高通滤波器
* 带通滤波器:允许一定范围频率通过并且允许其他频率通过
* 全通滤波器:允许所有频率通过，仅仅改变相位关系
* 陷波滤波器:阻止一个狭窄频率范围通过，是一种特殊带阻滤波器

### 滤波和模糊

* 高斯滤波是指用高斯函数作为滤波函数的滤波操作
* 高斯模糊就是高斯低通滤波

### 领域算子与现行邻域滤波

​	邻域算子(局部算子)是利用给定像素周围的像素值的决定此像素的最终值的一种算子。而线性邻域滤波就是一种常用的邻域算子，像素的输出值取决于输入像素的加权和

### 方块滤波

```c++
//函数原型
void boxFilter(InputArray src,OutputArray dst,intddepth,Size ksize,Point anchor= Point(-1,-1),bool normalize = true,int borderType = BORDER_DEFAULT)
```

* 第一个参数 ，`InputArray `类型的 `src`，输入图像，即源图像，填Mat类的对象即可。该函数对通道是独立处理的，而且可以处理热议通道数目的图片，待处理的图片深度应该为CV\_8U、CV\_16U、CV\_16S、CV\_32F、以及CV\_64F之一
* 第二个参数，`OutputArray` 类型的 `dst`，即目标图像，需要和源图片有一样的尺寸和类型
* 第三个参数，`int`类型的`ddepth`，输出图像深度，-1表示使用原图像深度，`src.depth`
* 第四个参数，`Size`类型的`ksize`，内核大小，一般用Size(w,h)表示内核大小，w代表像素宽度，h为像素高度
* 第五个参数，`Point`类型的`anchor`，表示锚点(被平滑的那个点)默认值为(-1,-1)如果为负值表示取核中心6+
* 第六个参数，`bool`类型的`normalize`，默认为true，一个标识符，表示内核是否被其区域归一化(normalized)了
* 第七个参数，`int`类型的`borderType1`，用于推断图像外部像素的某种边界模糊式，有默认，一般不去管它

`BoxFilter`函数方框滤波所有的核表示

$$
a\begin{vmatrix} 
1 &1&1&...&1&1 \\
1 &1&1&...&1&1 \\
...&...&...&...&...&...\\
1 &1&1&...&1&1 \\
\end{vmatrix}
$$
$a = 1$ OR $a = 1/(ksize.width*ksize.height)$

上式中f表示原图，h表示核，g表示目标图，当normalize = true 的时候，方框滤波就变成了我们熟悉的均值滤波，均值滤波是方框滤波的归一化后的特殊情况

归一化就是把要处理的量都缩放到一个范围内，比如(0 ,1)，以便于统一处理和直观量化。而非归一化的方框滤波用于计算每个像素邻域内的积分特性，而非归一化的方框滤波用于计算每个像素邻域内的积分特性，比如密集光流算法中用到的图像倒数的协方差矩阵

如果要在可变窗口中计算像素的总和，可以使用integral

## 快速上手API

```c++
void boxFilter(InputArray src,OutputArray dst,int ddepth,Size ksize,Point anchor=Point(-1,-1),bool normalize = true,int borderType=BORDER_DEFAULT)
```

```
//凸包绘制
#include<iostream>  
#include <vector>
#include <opencv2/opencv.hpp>
#include <opencv2/core/core.hpp>
#include<opencv2/imgproc/imgproc.hpp>

#include <opencv2/highgui/highgui.hpp> //highgui模块头文件
#include <opencv2/imgproc/imgproc.hpp> 

using namespace cv;
using namespace std;




int main(int argc,char**argv)
{
	Mat image(600, 600, CV_8UC3);
	RNG& rng = theRNG();
	while (true)
	{
		char key;
		int count;
		do
		{
			count = (unsigned)rng % 100 + 3;
		} while (count <= 0);
		vector<Point>points;
		for (int i = 0; i < count ;i++)
		{
			Point point;
			point.x = rng.uniform(image.cols / 4, image.cols* 3 / 4);
			point.y = rng.uniform(image.rows / 4, image.rows * 3 / 4);

			points.push_back(point);
		}
		vector<int>hull;
		convexHull(Mat(points), hull, true);
		image = Scalar::all(0);
		for (int i = 0; i < count; i++)
			circle(image, points[i], 3, Scalar(rng.uniform(0, 255),rng.uniform(0,255),rng.uniform(0,255)),CV_FILLED);
		int hullcount = (int)hull.size();
		Point point0 = points[hull[hullcount - 1]];
		
		for (int i = 0; i < hullcount; i++)
		{
			Point point = points[hull[i]];
			line(image, point0, point, Scalar(255, 255, 255), 2);
			point0 = point;
		}
		imshow("test", image);
		key = waitKey();
		if (key == 27)
			break;

	}
	

	waitKey(0);
	return 0;
}


```

```
#include<iostream>  
#include <vector>
#include <opencv2/opencv.hpp>
#include <opencv2/core/core.hpp>
#include<opencv2/imgproc/imgproc.hpp>

#include <opencv2/highgui/highgui.hpp> //highgui模块头文件
#include <opencv2/imgproc/imgproc.hpp> 

#define WINDOW_NAME1 "src_name1"
#define WINDOW_NAME2 "dst_name2"


using namespace cv;
using namespace std;

Mat g_srcImage;
Mat g_grayImage;
int g_nTreash = 50;
int g_maxTreash = 255;
RNG g_rng(12345);
Mat srcImage_copy = g_srcImage.clone();
Mat g_thresholdImage_output;
vector<vector<Point>> g_vContours;
vector<Vec4i>g_vHierarchy;

static void ShowHelpText();
void on_ThreshChange(int, void*);




int main(int argc,char**argv)
{
	g_srcImage = imread("finger2.jpg", 1);
	//imshow("win", g_srcImage);
	cvtColor(g_srcImage, g_grayImage, COLOR_BGR2GRAY);
	blur(g_grayImage, g_grayImage, Size(3, 3));

	imshow(WINDOW_NAME1, g_grayImage);

	createTrackbar("yu", WINDOW_NAME1, &g_nTreash, g_maxTreash, on_ThreshChange);
	on_ThreshChange(0, 0);

	waitKey(0);
	return 0;
}
void on_ThreshChange(int, void *)
{
	//bin 
	threshold(g_grayImage, g_thresholdImage_output, g_nTreash, 255, THRESH_BINARY);
	//find contours
	findContours(g_thresholdImage_output, g_vContours, g_vHierarchy, RETR_TREE, CHAIN_APPROX_SIMPLE, Point(0, 0));
	
	vector<vector<Point>>hull(g_vContours.size());
	for (signed int i = 0; i < g_vContours.size(); i++)
	{
		convexHull(Mat(g_vContours[i]), hull[i], false);
	}
	Mat drawing = Mat::zeros(g_thresholdImage_output.size(), CV_8UC3);
	for (unsigned int i = 0; i < g_vContours.size(); i++)
	{
		Scalar color = Scalar(g_rng.uniform(0, 255), g_rng.uniform(0, 255), g_rng.uniform(0, 255));
		drawContours(drawing, g_vContours, i, color, 1, 8, vector<Vec4i>(), 0, Point());
		drawContours(drawing, hull, i, color, 1, 8, vector<Vec4i>(), 0, Point());
	}
	imshow(WINDOW_NAME2, drawing);

}
shadowfly 
```

