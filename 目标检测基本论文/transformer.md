https://zhuanlan.zhihu.com/p/166608727

https://www.zhihu.com/question/337886108

**encoder输入输出**

让我们从输入开始，再从头理一遍单个encoder这个过程:

- 输入x
- x 做一个层归一化： x1 = norm(x)
- 进入多头self-attention: x2 = self_attention(x1)
- 残差加成：x3 = x + x2
- 再做个层归一化：x4 = norm(x3)
- 经过前馈网络: x5 = feed_forward(x4)
- 残差加成: x6 = x3 + x5
- 输出x6

![img](https://pic1.zhimg.com/80/v2-19aeff0b0eabd2f25941718d1785a734_720w.jpg)



decoder的输出：**输出是：**对应 ![[公式]](https://www.zhihu.com/equation?tex=\color{crimson}{i}) 位置的输出词的概率分布。

**输入是：** ![[公式]](https://www.zhihu.com/equation?tex=\color{purple}{Encoder}) **的输出** 和 **对应** ![[公式]](https://www.zhihu.com/equation?tex=\color{crimson}{i-1}) **位置decoder的输出**。所以中间的attention不是self-attention，它的Key和Value来自encoder，Query来自上一位置 ![[公式]](https://www.zhihu.com/equation?tex=\color{crimson}{Decoder}) 的输出。











self-attention：学习位置和内容关系

