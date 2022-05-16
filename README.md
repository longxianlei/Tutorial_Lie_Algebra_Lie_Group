# Tutorial_Lie_Algebra_Lie_Group
Tutorial on SLAM representing a moving scene in Lie algebra and Lie group.

重点参考的博文: 

[1. 李群与李代数对SLAM移动场景的运动坐标表示。](https://blog.csdn.net/qq_32998593/article/details/124801605?spm=1001.2014.3001.5501)

[2. 机器人与视觉——李群与李代数，李括号性质的分析与证明。](https://blog.csdn.net/qq_32998593/article/details/124684758?spm=1001.2014.3001.5501)

[3. How to represent a moving scene in SLAM.](https://blog.csdn.net/qq_32998593/article/details/124801605?spm=1001.2014.3001.5501)

## SLAM in representing a moving scene.

Representing a moving scene.

&emsp; **一些必须知识点**：skew matrix 是so(3)李代数中的，对应到SO(3)李群中的旋转矩阵R; twist matrix 是se(3)李代数中的，对应到SE(3)李群中的变换矩阵T。一些基本的知识点，skew matrix如何表达等，读者也应该了解。

&emsp; 本篇博文，将介绍，**李群与李代数的关系**，如何利用李群与李代数，构造便于表示的旋转/变换矩阵，来表示移动的场景和目标。
	
&emsp; 核心内容是：传统的**旋转矩阵R和变换矩阵T**，如果要在欧式空间进行构造，那么构造这个矩阵非常复杂，需要9个参数描述旋转，12个参数描述变换（9个旋转+3个平移）。而且，在欧式空间中，相机的移动，所依赖的变换矩阵，不是时间的变量，每次移动与上一次移动，其变换矩阵建立不起时间的联系，即微分方程。

&emsp; 因此，采用李代数，在tangent space中，**构造skew matrix: w^或者 twist matrix**，只需要极少的参数，skew matrix 只需要3维，twist matrix只需要6个参数。通过**指数映射**回李群，获得旋转矩阵/变换矩阵。从求解计算复杂度和参数的个数，都能明显的下降。

&emsp; 此外，相机的移动，对于李群中的矩阵，采用乘法来表示位姿点变化X1=TX0。而在李代数中，可以通过skew matrix 和 twist matrix来表示变换的**相对速度**，即当前时刻的3D坐标对时间的倒数，表示位姿（可以是相机的，可以是世界坐标系中目标点）的变换速度。任何的变换，在无穷小时间上看，都是微小的旋转/平移，因此，可以很方便的计算速度和位姿。

&emsp;下面，是通过对**李代数的介绍，指数映射，对数映射，刚体的旋转，刚体的变换（旋转+平移）**，随后给定参考坐标X0，移动相机，对场景进行拍摄，介绍如**何通过李代数来表示场景的移动过程**，参考的坐标点，在过程中，是如何随着相机移动变换的。
（这里不涉及到具体过程：如特征点提取，特征点匹配，ORB算法等，建立匹配点关系，求得变换矩阵等等。）

&emsp; 相对于前一篇[《机器人与视觉——李群与李代数，李括号性质的分析与证明》](https://blog.csdn.net/qq_32998593/article/details/124684758?spm=1001.2014.3001.5501)的博文，本文用文字来描述李群与李代数，及其对应的相机移动的运动表示应用。个人感觉这种方法，更能直观的理解，李群与李代数的原理，和为何选取这种表达方法来简化机器人、相机位姿求解问题。

### 1. Lie group and Lie algebra.

Using Lie algebra, we do not need to construct a complicated transformation matrix, which consist a 3x3 rotation matrix and a 3x1 translation vector. R is a rotation matrix satisfied R*RT=I. We only need 6 parameter, v and w. **And the matrix becomes 4x4 twist matrix.**

Taking the tangent space, and modeling the elements in Lie group (Rotation, Transformation) by corresponding element in the tangent space.
By introducing Lie algebra, we don't need explicitly construct a rotation matrix R with so many constraints. The 9 parameters in rotation matrix R can be represented by 3 parameters in w. Then, applied the exponential map to its skew matrix. We can get R. 

We summarize **the skew matrix** and **twist matrix** in **Lie algebra** and their **corresponding matrixs in the Lie group**, respectively.

#### 1.1 so(3)-> SO(3), only for rotation. 

##### 1.1.1 The exponential map.
##### 1.1.2 The Logarithm map.

#### 1.2 se(3)-> SE(3), for rigid-body motion.

### 2. The motion of the camera.
#### 2.1 Concatenation of motions over frame.
#### 2.2 Rules of velocity transformation.
#### 2.3 The adjoint map.
### 3. Summary.
**For more detailed information, please refer to the reference article.**
[How to represent a moving scene in SLAM.](https://blog.csdn.net/qq_32998593/article/details/124801605?spm=1001.2014.3001.5501)
