

位置编码

1d，2d实验证明差别不大



patch大小影响





多头机制

​	一组qkv得到了一组当前词的特征表达		多组多个特征，类似于CNN的多个卷积核通道

​    

![img](https://pic2.zhimg.com/80/v2-f784c73ae6eb34a00108b64e3db394fd_720w.jpg)

在self-attention的最后一部分我们来对比下self-attention和CNN的关系。如图19，今天在使用self-attention去处理一张图片的时候，1的那个pixel产生query，其他的各个pixel产生key。在做inner-product的时候，考虑的不是一个小的范围，而是一整张图片。

但是在做CNN的时候是只考虑感受野红框里面的资讯，而不是图片的全局信息。所以CNN可以看作是一种简化版本的self-attention。

或者可以反过来说，self-attention是一种复杂化的CNN，在做CNN的时候是只考虑感受野红框里面的资讯，而感受野的范围和大小是由人决定的。但是self-attention由attention找到相关的pixel，就好像是感受野的范围和大小是自动被学出来的，所以CNN可以看做是self-attention的特例，如图20所示。

![img](https://pic3.zhimg.com/80/v2-f28a8b0295863ab78d92a281ae55fce2_720w.jpg)图19：CNN考虑感受野范围，而self-attention考虑的不是一个小的范围，而是一整张图片

![img](https://pic4.zhimg.com/80/v2-f268035371aa22a350a317fc237a04f7_720w.jpg)图20：CNN可以看做是self-attention的特例

既然self-attention是更广义的CNN，则这个模型更加flexible。而我们认为，一个模型越flexible，训练它所需要的数据量就越多，所以在训练self-attention模型时就需要更多的数据，这一点在下面介绍的论文 ViT 中有印证，它需要的数据集是有3亿张图片的JFT-300，而如果不使用这么多数据而只使用ImageNet，则性能不如CNN。