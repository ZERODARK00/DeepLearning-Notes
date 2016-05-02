#Paper Reading——CNN
此部分主要是记录着我在CNN方面论文阅读的一些感想和笔记。

###A guide to convolution arithmetic for deep learning
* time:	2016-04-24
* author:	Vincent Dumoulin1 and Francesco Visin2
* content：介绍了卷积神经网络中kenrel size、kernel strides、input sizes、pooling size、pooling strides对于输出output size大小的影响关系。主要是围绕着卷积神经网络中对于图片处理后，图片的大小的一些思考。另外也有对于几种不同的padding的叙述。
	* Padding的种类如下，具体的图形解释如图。
		* No padding
		* Arbitrary padding
		* Half padding
		* Full padding 
	 
###Fractional Max-Pooling
* time:2016-05-01
* author:Benjamin Graham
* content:主要介绍了一种新的max pooling的方法。文章的目标在于减缓普通max pooling所带来的快速的图片feature尺寸的减小，最终导致了CNN网络无法更加deep。本文先分析pooling的本质是区域的划分（包括adjoint和overlapping两种类型），然后再将区域的划分归因到序列的产生上，从而可以根据（伪）随机序列来确定每一个pooling区域。

**两种pooling的方法——adjoint和overlapping的定义**

![Screenshot](https://github.com/zerodarkzerodark000000/DeepLearning-Notes/blob/master/NotesShortCuts/屏幕快照%202016-05-01%2021.27.11.png?raw=true)

**两种产生随机序列方法——随机法和伪随机法**

![Screenshot](https://github.com/zerodarkzerodark000000/DeepLearning-Notes/blob/master/NotesShortCuts/屏幕快照%202016-05-01%2021.27.29.png?raw=true)