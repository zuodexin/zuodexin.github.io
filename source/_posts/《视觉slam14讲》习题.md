---
title: 《视觉slam14讲》习题整理
date: 2020-11-08 22:53:12
tags: [CV]
mathjax: true
---

####  你知道C++11标准吗？你听说过或者使用过其中的那些特性？有没有其他标准？
[C++11新特性](https://cloud.tencent.com/developer/article/1745592#:~:text=%E5%85%B3%E4%BA%8EC%2B%2B11%E6%96%B0,%E6%8E%A8%E5%AF%BC%E5%87%BA%E5%8F%98%E9%87%8F%E7%9A%84%E7%B1%BB%E5%9E%8B%E3%80%82)
内容比较多，这要关注一下几点

##### 类型推导
auto和decltype关键字的引入，在编译时期推导出变量类型

##### 右值引用
[一文搞懂引用、指针、const、参数传递的关系](https://bbs.huaweicloud.com/blogs/267038)

关于`绑定`的概念

```c++
    const int& a = 1;
```
称为`把a绑定到1`


[一文读懂C++右值引用和std::move](https://zhuanlan.zhihu.com/p/335994370)
```c++
#include <iostream>
using namespace std;
int main() {
    int &&ref_a_right = 5; // ok
 
    int& a = ref_a_right;
 
    ref_a_right = 6; // 右值引用的用途：可以修改右值
	cout << a << "\n";
	return 0;
}
```
输出
```
6
```
右值指向左值用`std::move`


##### 列表初始化
[c++11 列表初始化](https://blog.csdn.net/hailong0715/article/details/54018002) c++98/03只支持普通数组和POD初始化，现在支持类的列表初始化

##### [std::function 和lambda表达式](https://zhuanlan.zhihu.com/p/137884434)
std::function 是可调用对象，可以存储
1. 自由函数
2. lambda表达式，`[capture list] (params list) mutable exception-> return type { function body }`，捕获变量的规则。
3. 存储bind调用结果，可调用对象和参数绑定，延迟调用
4. 其他函数调用

##### [智能指针](https://changkun.de/modern-cpp/zh-cn/05-pointers/index.html)
1. `shared_ptr<T>` 和 `make_shared<T>`
2. `unique_ptr<T>`
3. `week_ptr<T>`


#### 如何在Ubuntu中安装软件？这些软件被安装在什么地方？如果只知道模糊的软件名称，如何安装它？
`apt-cache search keyword`


#### 阅读文献【1】和【14】，你能看懂其中的内容吗？


#### g++的命令有哪些？怎么填写参数可以更改生成的程序文件名？
`-c` 编译

`-Ldir` 链接搜索库的路径

`-static` 禁止使用动态库

`-O[0,1,2,3]` -O0表示没有优化,-O1为缺省值，-O3优化级别最高

`-llibrary` 制定编译的时候使用的库

```
g++ -O output
```


#### 验证四元数旋转某个点后，结果是个虚四元数，所仍然对应到一个三维空间点
四元数的共轭$q^*=(s,-v_q)$
四元数的逆 $q^{-1}=q^*/||q^*||$
单位四元数旋转某个点的公式：$p'=qpq^{-1}$，


#### 画表总结旋转矩阵、轴角、欧拉角、四元数的转换关系

||旋转矩阵|轴角|欧拉角|四元数|
|-|-|-|-|-|
|旋转矩阵|-|罗德里格斯公式两边求迹|||
|轴角|$R=\cos{\theta}\mathbf{I}+(1-\cos{\theta})\mathbf{n}\mathbf{n}^T)+\sin{\theta}\mathbf{n}^{\wedge}$|-|||
|欧拉角|矩阵连乘||-||
|四元数|$R=\mathcal{v}\mathcal{v}^T+s^2I+2sv^{\wedge}+(v^{\wedge})^2$|左式求迹||-|

[三维旋转：欧拉角、四元数、旋转矩阵、轴角之间的转换](https://zhuanlan.zhihu.com/p/45404840)



#### 有个大的Eigen矩阵，想把它左上角3x3的块取出来赋值为$I_{3\times3}$,编程实现
关键的类MatrixXd,MatrixXf，成员方法block，类方法Random，Identity
```c++
#include<iostream>
#include<Eigen/Core>
using namespace std;
using namespace Eigen;



int main(int argc, char const *argv[])
{
    /* code */
    MatrixXd m=MatrixXd::Random(9,9);
    cout<<"before assign"<<endl;
    cout<<m<<endl;
    m.block(0,0,3,3) = Matrix3d::Identity();
    cout<<"after assign"<<endl;
    cout<<m<<endl;
    return 0;
}
```


####  AX=b求解有几种方法？在Eigen里实现

- QR分解，LU分解
- SVD分解的优点
- 理解广义逆求解
- 理解SVD求解推导


#### 验证SO(3),SE(3),Sim(3)关于乘法成群


#### 验证$(R^3,R,\times)$构成李代数


#### 验证$so(3)$ 和$se(3)$ 满足李代数要求的性质

#### 为什么高斯牛顿方法的增量方程可能不正定？不正定有什么几何含义？为什么在这种情况下解不稳定？


#### ORB、SIFT、SURF的原理。对比和ORB之间的优劣



#### 设计程序调用OpenCV其他种类的特征点，统计1000个特征点在你的机器上所用的时间。


#### 研究FLANN为何能快速处理匹配问题。出乱FLANN，还有哪些快速匹配的手段


#### 把演示程序所用的EPnP改成其他PnP方法，并研究他们的工作原理


<!--more-->