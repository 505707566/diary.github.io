# paa

# 2. Related Work



2.1基于概率分布的anchor分配策略



![image-20211221214042683](https://s2.loli.net/2021/12/21/xQRAWHytDwapiCb.png)

​		

​																																																lamuta是控制两者得分权重的

![image-20211221214407739](https://s2.loli.net/2021/12/21/JFyxBsfDa3Zq9He.png)

​																	定位评分  由IOU 来判断                                            f（）是基于该参数的模型								

​											![image-20211221214515569](https://s2.loli.net/2021/12/21/emu6sCZaQhU4l7P.png)

​						对总得分取负对数（缩小范围，乘法改成加法） =   分类loss（二元交叉熵损失）  和        定位loss（IOUloss）

​																													可以替换成 Focal loss和GIOU loss

为了分配一个anchor的正负样本。





用iou来作为训练和测试的框的质量

![image-20211221235214229](https://s2.loli.net/2021/12/21/VnWe7ZwEAF4N2bf.png)







推理的时候，iou作为nms的阈值

![image-20211221235825535](https://s2.loli.net/2021/12/21/oTtMSbzXcasfkC7.png)



