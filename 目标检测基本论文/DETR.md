DETR的Decoder主要有两个输入：

1. **Transformer Encoder输出的Embedding与 position encoding 之和。**
2. **Object queries。**

![image-20211116152421087](../../AppData/Roaming/Typora/typora-user-images/image-20211116152421087.png)

![image-20211116153115093](../../AppData/Roaming/Typora/typora-user-images/image-20211116153115093.png)

最重要的是q 

![image-20211116153639196](../../AppData/Roaming/Typora/typora-user-images/image-20211116153639196.png)

![image-20211116154354797](../../AppData/Roaming/Typora/typora-user-images/image-20211116154354797.png)

![image-20211116152421087](../../AppData/Roaming/Typora/typora-user-images/image-20211116152421087.png) ![image-20211116153115093](../../AppData/Roaming/Typora/typora-user-images/image-20211116153115093.png) 最重要的是q  ![image-20211116153639196](../../AppData/Roaming/Typora/typora-user-images/image-20211116153639196.png) ![](../../AppData/Roaming/Typora/typora-user-images/image-20211116154354797.png) 

多层加loss，

每一层保证后面每层都更好

