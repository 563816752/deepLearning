### Tensorflow 常用接口（卷积神经网络）

1. 卷积层

   **tf.nn.conv2d(input, filter, strides, padding, use_cudnn_on_gpu=None, name=None)**

   * input：指需要做卷积的输入图像，它要求是一个Tensor，具有[batch, in_height, in_width, in_channels]这样的shape，具体含义是[训练时一个batch的图片数量, 图片高度, 图片宽度, 图像通道数]，注意这是一个4维的Tensor，要求类型为float32和float64其中之一

   * filter：相当于CNN中的卷积核，它要求是一个Tensor，具有[filter_height, filter_width, in_channels, out_channels]这样的shape，具体含义是[卷积核的高度，卷积核的宽度，图像通道数，卷积核个数]，要求类型与参数input相同，有一个地方需要注意，第三维in_channels，就是参数input的第四维

   * strides：卷积时在图像每一维的步长，这是一个一维的向量，长度4

   * padding：string类型的量，只能是"SAME","VALID"其中之一，这个值决定了不同的卷积方式

     * SAME：

       ```python
       new_height = new_width = W / S    #结果向上取整
       ```

     * VALID

       ```python
       new_height = new_width = (W – F + 1) / S  #结果向上取整
       ```

       ​

   * use_cudnn_on_gpu:bool类型，是否使用cudnn加速，默认为true

   * 结果返回一个Tensor，这个输出，就是我们常说的feature map，shape仍然是[batch, height, width, channels]这种形式。

   ​