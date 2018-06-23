## TextCNN论文理解

论文地址[Convolutional Neural Networks for Sentence Classification](https://arxiv.org/pdf/1408.5882v2.pdf)

卷积神经网络（CNN）来自于计算机视觉领域。它的主要思想是使用许多一小段一小段的卷积滤波器（convolving filters）施加到二维图像上，在图像上沿着x、y轴不断滚动，发现局部特征。可以有很多滤波器，每个卷积滤波器负责各自的特征提取。因为卷积滤波器参数共享的机制，相比于全连接（Full Connection）参数个数大大减少，降低了过拟合的风险。

在本文中，一个句子（Sentence）是一个一维的结构，可以通过单词向量化变成二维结构。向量化的方法，文中比较了随机映射法和[word2vec](https://arxiv.org/pdf/1301.3781.pdf)法。当然word2vec有更好的效果。结构图如下：

