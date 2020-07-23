# Three-Chamber
基于 three.js 做的一些程序和学习示例。</br>
体验地址：
1.三阶魔方 https://wwjll.github.io/Three-Chamber/Rubik/RubikClass.html </br>
2.超立方体 https://wwjll.github.io/Three-Chamber/HyperCube/HyperCube.html </br>
# Rubik
魔方程序，包括步骤过程，GUI面板控制（todo），阶数变换,改写成 class 类等。clone 后可以直接打开 html 文件试验效果。 </br>
原始的三阶魔方实现方法来自 https://zhuanlan.zhihu.com/p/33580374, 本人学习后进行改写和扩充。 </br>
有兴趣可以跟着文章从头实现，有遇到四元数旋转或其他较难理解的概念可参考以下描述。 </br>
里面有多个 html 文件，程序有注释，可运行后自己调试。 </br>
# HyperCube
展示了4 维超立方体围绕 XYZW 超平面旋转投影到 3 维的影像。放大后效果更佳 </br>
实现要点：</br>
    1.对于立方体，每增加一个维度，相当于原本的立方体向垂直于原先所有坐标轴的新轴平移产生的形状（比如正方形拉伸变成正方体）。因而可以定义坐标(x, y, z, w)。</br>
    2.要获得立体旋转效果需要采用透视投影而不是正交投影，物理意义在于沿着新的 w 轴透视投影，采用归一化坐标，
    定义距离 distance = 2, w = 1/(distance - v.w),其中 v 为 4 维坐标向量。</br>
    3.计算坐标。新坐标先旋转再投影，参见代码实现，不明白可以网上搜索相关内容。THREE 中没有 4*3 矩阵与相关向量的运算，需要自行定义，本代码中仅仅定义了所需的矩阵和向量运算，其实可以定义任意符合计算法则(矩阵的列数等于向量的行数)的矩阵和向量相乘。</br>
    4.Line 对象更新旋转后的坐标。</br>
    5.基于这套方法，理论上可以从 n 维旋转再依次投影到 n-1,直到 3 维,有兴趣可以进一步探索实验（计算量暴增警告）。
    值得一提的是我们在屏幕上看到的 3D 效果其实都是模拟出来的，也就是 (x,y,z) 投影到屏幕 (x,y) 的过程。</br>

## 前置知识
1.threejs 基本对象的使用</br>
2.Threejs 获取和使用旋转四元数</br>
    1.获得两向量的单位法向量（旋转轴）axis </br>
    2.旋转的弧度 rad </br>
    3.通过 quaternion.setFromAxis（axis，rad）获取。 </br>
    4.面上每个元素 premiltiply 四元数后还要再作欧拉旋转（绕原点旋转，可以想象成如行星绕恒星转动，自传加公转）</br>
3.其他和补充说明 </br>
    四元数的基本知识和性质 </br>
        1.四维坐标刚体运动可在三维坐标里表示为两个三维运动，三维视为四维投影。三维坐标转换为四元数 p 后，左乘旋转四元数q可得旋转后的效果，但是被拉伸了，再右乘q-1后则可以消除拉伸效果，q-1也被视作旋转轴。同方向和角度转动了两次，因而求得的旋转四元数是要转动角度 a 的一半 a/2。</br>
        2.使用旋转四元数 p 对三维坐标 q 进行转动时，当转动轴为三个坐标轴的单位向量时，只需要 q 左乘 p。</br>
        3. 四元数   Q(p,v)   v =(x,y,z)共轭  即为： Q*(p,-v);轴和 四元数  是反向的四元数   Q(p,v),   v =(x,y,z)。 Q逆为：Q*/四元数长度。</br>
        
4.更直观地理解四元数可以自行搜索 3b1b 等人制作的关于四元数的视频。</br>
5.矩阵与向量的运算法则。</br>

