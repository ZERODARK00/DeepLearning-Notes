#Deep	Learning Notes
在这里将会存放我在阅读《Deep Learning》这本书中或者是学习深度学习网络课程中，所产生的疑问、感想以及灵感等方面的内容，同时也会梳理有关书籍中的一些知识点，作为我的学习笔记本。
##Convolution Neural Network
卷积神经网络是比较早出现在深度学习领域的一种网络，主要用作图像识别（CV）领域，但是也在人们的集思广益下得到了普世性的发展。因此目前神经网络的领域也是越来越广泛，主要有图像、声音等。
###2016-04-20 GET
对于卷积神经网络的推导以及实现，可以参考文章[**《Deep Learning论文笔记之（四）CNN卷积神经网络推导和实现》**](http://blog.csdn.net/zouxy09/article/details/9993371),这篇文章从原理上解释了神经网络的数学计算方式，并且在后续的教程中提供了MATLAB代码的解读。以下是当天的学习所获：

**Pooling的意义：**

* *可以忽视像素移动对整个图像特征提取的影响。以max pooling为例，由于是周围的几个像素共同影响pooling后的结果，因此平移后对于最后的结果将要比不pooling所得结果变化小得多。*
* *可以忽略图像旋转对整个图像特征提取的影响。*
* *可以减小图像的size，提高计算效率*

**卷集中变量维度表示**

*When working with images, we usually think of the input and output of the convolution as being 3-D tensors, with one index into the different channels（有多少源） and two indices into the spatial coordinates of each channel（长宽等信息）. Software implementations usually work in batch mode, so they will actually use 4-D tensors, with the fourth axis indexing different examples in the batch（最后一维是一次训练数据集大小）, but we will omit the batch axis in our description here for simplicity.*
###2016-04-21 GET
主要观看了google上的有关深度学习的网络课程，该课程偏于应用工程方面，因此对于一些训练的技巧或者是所需要的概念的解释是比较深入人心的。

**Regulazation的方法**

* *在Loss函数后添加***权重2范数项***，最小化改进后的Loss函数*
* *Dropout方法：上一层输出随机数据进行丢失后，作为下一层输入*
	* *优点之一：CNN中大量共享全值，因此随机丢失数据，不会带来过严重的数据丢失，反而可以去除冗余*
	* *优点之二：计算速度会有一定的提升*

**关于网络结构的疑问**

* RELU作为激活函数，那么其输入以及输出是什么，有怎样的意义？
	* *根据目前所掌握的情况来看，RELU是通过输入的多个map中对应的像素值来生成一个像素值，因此应该是属于POOLing的一种情况*

**Statistic Invariance**

正是由于数据中存在无关项的因素，从而提出了卷积神经网络的概念，从而来消除这些干扰信息，提高训练效果。具体相关的数据中的无关项如下所示：

* 颜色不影响对分类没有重大的影响
* 图像、单词的位置对于分类没有重大影响

**CNN术语解释**

* FeatureMap（depth）：某一层网络的对于图片提取出的某一个特征
* Patch（Kernel）：进行卷积操作的特征提取器
* stride：特征提取器width、height两方向各自每一次移动的的pixel数，例如strides=1最后提取出来的FeatureMap与原有输入等大（same padding情况下）
* Valid padding：输出与输入不等大，一般输出小于输入
* Same padding：输出与输入等大（包括width、height）

###2016-05-02 GET
**Quora上看到的精彩的回答：**

1.***[How does the <mark>dropout</mark> method work in deep learning?](https://www.quora.com/How-does-the-dropout-method-work-in-deep-learning)***

> **Dropout is a form of regularisation.**
>
> How does it work?
> 
> It essentially forces an artificial neural network to learn multiple independent representations of the same data by alternately randomly disabling neurons in the learning phase.
>
> What is the effect of this?
> 
> The effect of this is that neurons are prevented from co-adapting too much which makes overfitting less likely.
>
>Why does this happen?
>
>The reason that this works is comparable to why using the mean outputs of many separately trained neural networks to reduces overfitting.

**Dropout是正则化的一种方法。**

* 它如何工作？

***Dropout通过禁止学习阶段的神经元来强迫学习同一数据的多种不同的表达***

* 它的影响是？

***阻止了过度的共同适应（协同学习），从而减少了过拟合的可能性***

* 为什么需要它

***减少过拟合***

2.***[Why does batch <mark>normalization</mark> help?](https://www.quora.com/Why-does-batch-normalization-help)***
>Batch normalization potentially helps in two ways:  faster learning and higher overall accuracy.  The improved method also allows you to use a higher learning rate, potentially providing another boost in speed.

>Why does this work?  Well, we know that normalization (shifting inputs to zero-mean and unit variance) is often used as a pre-processing step to make the data comparable across features.  As the data flows through a deep network, the weights and parameters adjust those values, sometimes making the data too big or too small again - a problem the authors refer to as "internal covariate shift".  By normalizing the data in each mini-batch, this problem is largely avoided.

>Basically, rather than just performing normalization once in the beginning, you're doing it all over place.  Of course, this is a drastically simplified view of the matter (since for one thing, I'm completely ignoring the post-processing updates applied to the entire network), but hopefully this gives a good high-level overview.


