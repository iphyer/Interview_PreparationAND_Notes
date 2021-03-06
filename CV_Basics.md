
Summary of CV Problems in Interview

# Question List

# Questions



## Q17 1x1 卷积的作用

第三轮是ML breadth，从clustering， SVM， PCA blabla一直考到Bayesian AB testing，random forest etc，基本上我简历上提到的都考了。. From 1point 3acres bbs
第四轮是hiring manager面的ML case，也主要是针对我以前做的project细问，如何改进，如何更personalization，还问了问我有没有sprint planning的经验
第五轮是ML depth，面试官让我挑一个我自认为比较擅长的领域（classification，regression， causal impact之类的都行），然后细问，比如loss function啊，什么情况下该选什么。最后还问了一下word2vec具体怎么做的


Edge detection
1. edge产生的原因
相机成像的过程，光线从光源照射到物体的表面，发生了吸收和反射，反射的光线被感光元件接收，将强度信息转化成为信号的强度，从而显示为图像。
edge主要是接收到的光线强度的不连续而产生的，具体的，造成的原因可能有物体表面的反射特性不同，即有些区域反射的强度大而有些区域反射的强度小。同时，基于表面的反射特性以及物体和入射光线夹角的不同，发射光的强度的变化，产生edge。而造成这一夹角的变化，可能是由于物体的形状，也可能是物体和光源的距离。除此之外，光源的不连续分布也可能产生edge，利于明暗的边界和阴影。
2. 如何去检测图像中的edge
既然edge是强度的不连续分布，直观上，我们可以去计算图像的强度梯度信息。具体的，我们可以去计算一阶和二阶梯度信息，对于一阶梯度图，edge对应的是local extrama，而对于二阶梯度图，edge对应的过零点。
一个常见的问题是图像中往往存在噪声，噪声在一阶梯度图中同样对应的是local extrama，从而影响对真实edge的检测。一个常规的做法是先对图像进行滤波降噪，比如高斯滤波，然后在计算梯度信息。由于高斯滤波和梯度计算都是线性变换，我们可以将其合并简化。
3. edge的拟合
通常，梯度图检测到的edge信息是一个点集，即不连续，由此，我们需要用曲线去拟合这些点。最常见的方法是最小二乘法，假设一个多项式分布，然后利用梯度下降去最小化误差。但是这对于多模态的分布不适用 （或许可以用maximum expectation）。一个更加有意思的算法是hough transform，基本原理是就是假定一个图像空间和一个分布对应的参数空间，然后图像空间的每个点都可以映射到参数空间的一个分布，最后通过在参数空间的majority voting求取分布。hough transform适用于一个简单的低维的分布。generalized hough transform可以应用于一些特定的复杂分布，但是不常用。
4. edge和corner
在计算机视觉领域，检测corner也是一个很有意思的工作，尤其在boundary detection上。这里，我们可以利用edge检测器去寻找corner。通常的，corner可以认为是两条相交的edge组成的。由此，如果我们在图像中随机选取一个小的图像快，计算梯度图，然后统计梯度的分布信息（强度和方向）。如果分布是各向同性，则图像块中不存在edge和corner。如果分布中有一个信号特别强的方向，则图像块包含edge。如果分布中有两个特别强的方向，则图像块中包含corner。
5. active boundary refinement
就是当我们有了一个粗略估计的boundary之后，如何去计算更加精准的boundary。这其实是一个优化问题，目标函数包含了三项，外在牵引力，内在的弹性和平滑性。具体点，一个boundary可以用点集来表示，其中的每个点会受到梯度图中的edge的牵引力，同时我们要求edge应该是连续且平滑的，即一阶和二阶导数不能太大。
6. scale invariant 和 sift
如果假设edge是圆形分布，那么，在拉普拉斯算子下，信号会有一个特性，即存在一个sigma使得信号在归一化拉普拉斯算子下达到local maxima。基于此，我们可以在图像中寻找这一类的特征点，并且计算每个特征点对应的sigma。特别的，sigma对应的是edge的scale。
大体上，sift算法就是基于这一发现而提出的。特别的，sift算法利用高斯算子的差来近似拉普拉斯算子，提高了计算的效率。同时，对于每个特征点对应的scale，sift利用hog来计算特征向量，从而提高了特征点匹配的准确性和鲁棒性。

在计算机视觉领域，检测corner也是一个很有意思的工作，尤其在boundary detection上。这里，我们可以利用edge检测器去寻找corner。通常的，corner可以认为是两条相交的edge组成的。由此，如果我们在图像中随机选取一个小的图像快，计算梯度图，然后统计梯度的分布信息（强度和方向）。如果分布是各向同性，则图像块中不存在edge和corner。如果分布中有一个信号特别强的方向，则图像块包含edge。如果分布中有两个特别强的方向，则图像块中包含corner。


## 18. Pytorch 如何做卷积计算？


![Pytorch_Conv_Img](https://github.com/iphyer/MLE_Interview_Preparation/blob/main/Resources/Pics/pytorch_conv.jpeg)

## 19. Feature Pyramid Network (FPN) 如何提高小物体检测？

1. 多尺度视角帮助得到更多的信息，比如小尺寸的物体
2. Conv 操作会对信息作抽象，损失细节，所以 FPN 可以得到更细节信息。
