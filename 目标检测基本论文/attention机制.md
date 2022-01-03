RNN with Attention
在nlp领域，attention主要应用在Encoder + Decoder框架的基础上。
attention最早应该出现在2014年bengio的neural machine translation论文上面，在seq2seq问题上引入attention

CNN with Attention
主要分为两种，一种是spatial attention, 另外一种是channel attention。
CNN每一层都会输出一个C x H x W的特征图，C就是通道，代表卷积核的数量，亦为特征的数量，H 和W就是原始图片经过压缩后的图，spatial attention就是对于所有的通道，在二维平面上，对H x W尺寸的图学习到一个权重，对每个像素都会学习到一个权重。你可以想象成一个像素是C维的一个向量，深度是C，在C个维度上，权重都是一样的，但是在平面上，权重不一样。这方面的论文已经很多了，重点关注一下image/video caption。相反的，channel attention就是对每个C，在channel维度上，学习到不同的权重，平面维度上权重相同。spatial 和 channel attention可以理解为关注图片的不同区域和关注图片的不同特征。channel attention写的最好的一篇论文是SCA-CNN

网络架构上，Squeeze and Excitation Network就是channel attention的典型代表，主要思想是卷积网络的卷积核所代表的特征之间存在冗余，他们起了个名字叫feature recalibration，可以看作是在不影响性能的前提下减少卷积核数量是等效的。
patial transformer networks (STN) 是之后将attention用于物体识别比较有名的一篇文章，在一些现实应用中仍被使用。再如residual attention network.

attention机制听起来高达上，其实就是学出一个权重分布，再拿这个权重分布施加在原来的特征之上，就可以叫做attention。简单来说：
（1）这个加权可以是保留所有分量均做加权（即soft attention）；也可以是在分布中以某种采样策略选取部分分量（即hard attention）。

（3）这个加权可以作用在空间尺度上，给不同空间区域加权；也可以作用在channel尺度上，给不同通道特征加权；甚至特征图上每个元素加权。
（4）这个加权RNN with Attention

在nlp领域，attention主要应用在Encoder + Decoder框架的基础上。
attention最早应该出现在2014年bengio的neural machine translation论文上面，在seq2seq问题上引入attention

#### CNN with Attention

主要分为两种，一种是spatial attention, 另外一种是channel attention。
CNN每一层都会输出一个C x H x W的特征图，C就是通道，代表卷积核的数量，亦为特征的数量，H 和W就是原始图片经过压缩后的图，spatial attention就是对于所有的通道，在二维平面上，对H x W尺寸的图学习到一个权重，对每个像素都会学习到一个权重。你可以想象成一个像素是C维的一个向量，深度是C，在C个维度上，权重都是一样的，但是在平面上，权重不一样。这方面的论文已经很多了，重点关注一下image/video caption。相反的，channel attention就是对每个C，在channel维度上，学习到不同的权重，平面维度上权重相同。spatial 和 channel attention可以理解为关注图片的不同区域和关注图片的不同特征。channel attention写的最好的一篇论文是SCA-CNN

网络架构上，Squeeze and Excitation Network就是channel attention的典型代表，主要思想是卷积网络的卷积核所代表的特征之间存在冗余，他们起了个名字叫feature recalibration，可以看作是在不影响性能的前提下减少卷积核数量是等效的。
patial transformer networks (STN) 是之后将attention用于物体识别比较有名的一篇文章，在一些现实应用中仍被使用。再如residual attention network.

attention机制听起来高达上，其实就是学出一个权重分布，再拿这个权重分布施加在原来的特征之上，就可以叫做attention。简单来说：
（1）这个加权可以是保留所有分量均做加权（即soft attention）；也可以是在分布中以某种采样策略选取部分分量（即hard attention）。

（3）这个加权可以作用在空间尺度上，给不同空间区域加权；也可以作用在channel尺度上，给不同通道特征加权；甚至特征图上每个元素加权。
（4）这个加权还可以作用在不同时刻历史特征上，如Machine Translation，以及我前段时间做的视频相关的工作。

![img](https://img-blog.csdnimg.cn/20191227160457166.png)还可以作用在不同时刻历史特征上，如Machine Translation，以及我前段时间做的视频相关的工作。

————————————————
版权声明：本文为CSDN博主「NCU_wander」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/NCU_wander/article/details/103733756