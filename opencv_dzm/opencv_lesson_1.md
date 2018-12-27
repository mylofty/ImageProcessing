# opencv 基础一
## 一、Mat
1、早期的opencv管理图片使用的是结构体IplImage (Image processing Library Image)，然而，跟大多数C程序一样，需要用户手动分配和回收内存，容易出错，不利于程序小型化。

2、Mat是一个C++类，使用者不需要手动去分配和回收内存，（当然早期的代码有的仍然先用IplImage分配内存），Mat包含两部分：(1).矩阵头部（包括矩阵大小，存储位置等），(2).指向内存中像素点的指针

3、**内存管理:** Mat类包含header和pointer，其中，pointer指向一个堆，Mat类管理的图片像素矩阵其实存在这个区域，所以，当进行**复制**和**赋值**操作时，副本中仅仅生成新的header和pointer，图片像素矩阵不会拷贝一份(**浅拷贝**)，pointer类似使用智能指针，通过增加引用计数的方式，只有计数为0才会删除像素内存，所以O（1）时间完成拷贝。
```c++
Mat A, C;
A = imread(argv[1], IMREAD_COLOR);
Mat B(A);  		// 调用拷贝构造函数，不复制图像内存
C = A;			// 执行赋值操作，不复制图像内存
```
若是需要拷贝图片像素矩阵，则需要使用**cv::Mat::clone() ** 和 ** cv::Mat::copyTo() ** 函数
```
Mat F = A.clone();
Mat G;
A.copyTo(G);
```

4、Mat常用构造方法
（1）、构建二维矩阵
```c++
Mat M(20, 20, CV_8UC3, Scalar(0,0,255))  
// 构建20×20图像，每个像素8bit， 3通道， 初始化为（0,0,255），BGR 红色
cv::imshow("M picture", M);
```
（2）、构建多维矩阵
```
cv::Mat L(3, sz, CV_8UC1, cv::Scalar(0));
// 多维矩阵无法cout和imshow，没有重载
```
（3）、创建固定形式矩阵
```
Mat E = Mat::eye(4, 4, CV_64F);
Mat o = Mat::ones(2, 2, CV_32F);
Mat Z = Mat::zeros(3, 3, CV_8UC1);
```