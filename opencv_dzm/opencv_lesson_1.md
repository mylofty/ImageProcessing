# opencv 基础一
## 一、Mat
1、早期的opencv管理图片使用的是结构体IplImage (Image processing Library Image)，然而，跟大多数C程序一样，需要用户手动分配和回收内存，容易出错，不利于程序小型化。

2、Mat是一个C++类，使用者不需要手动去分配和回收内存，（当然早期的代码有的仍然先用IplImage分配内存），Mat包含两部分：(1).矩阵头部（包括矩阵大小，存储位置等），(2).指向内存中像素点的指针

3、**内存管理:** Mat类包含header和pointer，其中，pointer指向一个堆，Mat类管理的图片像素其实存在这个区域，所以，当进行**复制**和**赋值**操作时，副本中仅仅生成新的header和pointer，图片像素数据不会拷贝一份(**浅拷贝**)
```c++
Mat A, C;
A = imread(argv[1], IMREAD_COLOR);
Mat B(A);  		// 调用拷贝构造函数，不复制图像内存
C = A;			// 执行赋值操作，不复制图像内存
```