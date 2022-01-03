![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108104811520.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6bXNodWFp,size_16,color_FFFFFF,t_70)

其中 X t X_{t}X 
t

 表示 第 t tt 帧视频帧输入到CNN网络中输出的feature map，尺寸为 K × K × C K\times K\times CK×K×C，其中K表示feature map的空间尺寸，C表示feature map的channel维度。l t l_{t}l 
t

  表示第t帧对应的注意力图，大小为 K ∗ K K* KK∗K的向量，注意力图与卷积特征图相结合得到x t x_{t}x 
t

 ，为当前时刻LSTM网络的输入。LSTM网络的输出经过tanh非线性变换后作为整个网络当前时刻的输出。整个网络的结构就是这样，下面会更加详细地介绍网络各个模块的计算方法。

注意力图（attention map）的计算
我们知道注意力图是要与CNN feature map 进一步结合的，那么 attention map 的大小为什么为K ∗ K K* KK∗K的向量呢？因为CNN输出的卷积特征图的尺寸为K × K × C K\times K\times CK×K×C，如果沿着feature map的空间维度展开，可以看成是 k×k个d维的向量，每一个向量对应着输入视频帧中不同区域的卷积特征值，之前说过我们添加注意力机制的目的是让网络能够关注视频帧中与行为类别相关的区域，所以attention map 的尺寸应该与feature map的空间尺寸一一对应，从而加强感兴趣区域卷积特征，减小或忽略不感兴趣区域的卷积特征。
attention map的计算方法如下式所示：

可以看到其是根据前一时刻最高层的LSTM的隐藏单元计算而来，其实就是相当于将h t − 1 h_{t-1}h 
t−1

 输入到全连接层中，得到输出再经过softmax层，最终得到的就是注意力图attention map l t l_{t}l 
t

 ，全连接的尺寸为H × K ∗ K H\times K*KH×K∗K。
————————————————
版权声明：本文为CSDN博主「NRZZN」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/zzmshuai注意力图（attention map）的计算

我们知道注意力图是要与CNN feature map 进一步结合的，那么 attention map 的大小为什么为K ∗ K K* K*K*∗*K*的向量呢？因为CNN输出的卷积特征图的尺寸为K × K × C K\times K\times C*K*×*K*×*C*，如果沿着feature map的空间维度展开，可以看成是 k×k个d维的向量，每一个向量对应着输入视频帧中不同区域的卷积特征值，之前说过我们添加注意力机制的目的是让网络能够关注视频帧中与行为类别相关的区域，所以attention map 的尺寸应该与feature map的空间尺寸一一对应，从而加强感兴趣区域卷积特征，减小或忽略不感兴趣区域的卷积特征。
attention map的计算方法如下式所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108111140430.png)

## attention=空间注意力（每个通道的总占比）



可以看到其是根据前一时刻最高层的LSTM的隐藏单元计算而来，其实就是相当于将h t − 1 h_{t-1}*h**t*−1​输入到全连接层中，得到输出再经过softmax层，最终得到的就是注意力图attention map l t l_{t}*l**t*​，全连接的尺寸为H × K ∗ K H\times K*K*H*×*K*∗*K*。/article/details/86063410