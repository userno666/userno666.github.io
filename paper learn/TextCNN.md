## TextCNN论文理解

论文地址[Convolutional Neural Networks for Sentence Classification](https://arxiv.org/pdf/1408.5882v2.pdf)

卷积神经网络（CNN）来自于计算机视觉领域。它的主要思想是使用许多一小段一小段的卷积滤波器（convolving filters）施加到二维图像上，在图像上沿着x、y轴不断滚动，发现局部特征。可以有很多滤波器，每个卷积滤波器负责各自的特征提取。因为卷积滤波器参数共享的机制，相比于全连接（Full Connection）参数个数大大减少，降低了过拟合的风险。

在本文中，一个句子（Sentence）是一个一维的结构，可以通过单词向量化变成二维结构。向量化的方法，文中比较了随机映射法和[word2vec](https://arxiv.org/pdf/1301.3781.pdf)法。当然word2vec有更好的效果。结构图如下：

![image](https://userno666.github.io/paper%20learn/2018-06-23%2014-06-32屏幕截图.png)

先讨论第一部分。文中同时比较了静态（static）和动态（non static）的词向量，区别就是静态词向量是固定不变的，而动态词向量在训练过程中可以调节，这个调节过程在文中叫Fine Tune。对于未登录词，通常用随机小量。这样就形成了第一部分的二维结构。但是和图像卷积中的不同之处是，卷积滤波器通常不会同时在两个方向上移动，毕竟词向量拆散了没有任何意义对不对，所以只能沿着纵轴卷积，而横轴则和卷积滤波器长度一样。论文中说经过网格搜索（grid search），卷积窗口的大小（filter windows）通常在3、4、5，也就是说最多可以利用邻近4个单词的信息。（个人觉得这里可能是CNN应用在文本的一个局限吧，文本中的长距离影响还是很多的）。

接下来是池化层。文中使用了Max-over-time Pooling的方法，就是简单的选择最大值。

接下来和普通的CNN大同小异。一层全连接，一层Softmax。在全连接可以使用drop out，当然在预测时使用全部参数要乘以keep_prob。

根据文中的实验结果，CNN-static(经过word2vec)比CNN-rand有较大提升。CNN-static\CNN-non-static\CNN-multichannel则各有千秋。比较有趣的是，文中还把CNN-non-static经过fine-tune的词向量进行了比较：

![fine tune后的词向量](https://userno666.github.io/paper%20learn/2018-06-23%2014-48-44屏幕截图.png)
原本bad和good有相似的句法结构，所以在原始词向量中它们较为接近。而经过fine tune后，则这一明显违反事实的现象明显得到了改观。

接下来，针对不能解决长距离词语的相互作用的问题，我会看一下DCNN（Dynamic Convolutional Neural Network）的论文。
