SSD与MTCNN的不同
生成训练数据的方式不同
MTCNN需要事先手动将所有的训练样本生成好，然后输入到网络中训练, 而SSD不需要，SSD在训练过程中自动生成所有训练样本。SSD中实际的训练样本就是所有anchor，每个anchor的label由anchor与ground truth匹配来确定。SSD实现了真正意义上端到端的训练。
MTCNN和SSD采用了两种不同的多尺度检测策略
MTCNN：首先构建图像金字塔，然后使用固定大小的滑动窗口在金字塔每一级滑动，对每个滑动窗口分类回归。
SSD: 在原图中设置了不同大小的滑动窗口，对不同大小的滑动窗口进行分类和回归。
不管是MTCNN，还是SSD，本质上是对所有滑动窗口的分类。这与传统的目标检测方法本质上是一样的。
Mining的方式不同
MTCNN需要手动做mining,而SSD采用了OHNM训练过程中自动完成负样本的mining，解决了简单样本的问题和类别不平衡问题。
其实MTCNN中也是有anchor的， MTCNN中的anchor就是PNet的滑动窗口
MTCNN的训练样本就是滑动窗口图像，而生成训练样本的时候使用滑动窗口与groundtruth进行匹配，得到分类和回归的label，所以anchor就是PNet的滑动窗口。不过与SSD的区别在于这个匹配过程不是训练过程中自动完成的，而是事先手动完成。
判断什么是anchor的方法：使用什么匹配groundtruth的，那个就是anchor
————————————————
版权声明：本文为CSDN博主「qianqing13579」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qianqing13579/article/details/82106664

SSD的缺点及改进
1. SSD主要缺点：SSD对小目标的检测效果一般，作者认为小目标在高层没有足够的信息。

论文原文：
This is not surprising because those small objects may not even have any information at the very top layers. Increasing the input size (e.g. from 300× 300 to 512× 512) can help improve detecting small objects, but there is still a lot of room to improve.

对小目标检测的改进可以从下面几个方面考虑：
1. 增大输入尺寸
2. 使用更低的特征图做检测(比如S3FD中使用更低的conv3_3检测)
3. FPN(已经是检测网络的标配了)

2. 关于anchor的设置的优化

An alternative way of improving SSD is to design a better tiling of default boxes so that its position and scale are better aligned with the receptive field of each position on a feature map. We leave this for future work. P12
论文中提到的anchor设置没有对齐感受野，通常几个像素的中心位置偏移，对大目标来说IOU变化不会很大，但对小目标IOU变化剧烈，尤其感受野不够大的时候，anchor很可能偏移出感受野区域，影响性能。
关于anchor的设计，作者还提到了
In practice, one can also design a distribution of default boxes to best fit a specific dataset. How to design the optimal tiling is an open question as well
论文提到根据特定数据集设计default box，在YOLOV2中使用聚类的方式初始化anchor，能够更好的匹配到ground truth,帮助网络更好的训练
————————————————
版权声明：本文为CSDN博主「qianqing13579」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qianqing13579/article/details/82106664

SSD 与最初的两个模型（faster rcnn、rfcn）并无不同。它简单跳过「region proposal」这一步，而不是同时考虑图像每个位置的每个边界及其分类。由于 SSD 一次性完成所有，它是三个模型中最快的，且相对而言依然表现出色。