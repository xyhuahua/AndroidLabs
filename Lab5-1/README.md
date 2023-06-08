# 使用TensorFlow Lite Model Maker生成图像分类模型
## 预备工作

首先安装程序运行必备的一些库。
 pip install -i https://pypi.tuna.tsinghua.edu.cn/simple tflite-model-maker      
 
![](https://huatu.98youxi.com/markdown/work/uploads/upload_16747632a077c91d79dcaf866305371d.png)


接下来，导入相关的库。

```python
import os

import numpy as np

import tensorflow as tf
assert tf.__version__.startswith('2')

from tflite_model_maker import model_spec
from tflite_model_maker import image_classifier
from tflite_model_maker.config import ExportFormat
from tflite_model_maker.config import QuantizationConfig
from tflite_model_maker.image_classifier import DataLoader

import matplotlib.pyplot as plt

```

## 模型训练
### 获取数据
模型训练
获取数据
本实验先从较小的数据集开始训练，当然越多的数据，模型精度更高。
```python=
image_path = tf.keras.utils.get_file(
      'flower_photos.tgz',
      'https://storage.googleapis.com/download.tensorflow.org/example_images/flower_photos.tgz',
      extract=True)
image_path = os.path.join(os.path.dirname(image_path), 'flower_photos')

```
这里从`storage.googleapis.com`中下载了本实验所需要的数据集。`image_path`可以定制，默认是在用户目录的`.keras\datasets`中。

## 运行示例

一共需4步完成。  
第一步：加载数据集，并将数据集分为训练数据和测试数据

```python=
data = DataLoader.from_folder(image_path)
train_data, test_data = data.split(0.9)

```
第二步：训练Tensorflow模型
```python=
INFO:tensorflow:Retraining the models...
Model: "sequential"
_________________________________________________________________
 Layer (type)                Output Shape              Param #   
=================================================================
 hub_keras_layer_v1v2 (HubKe  (None, 1280)             3413024   
 rasLayerV1V2)                                                   
                                                                 
 dropout (Dropout)           (None, 1280)              0         
                                                                 
 dense (Dense)               (None, 5)                 6405      
                                                                 
=================================================================
Total params: 3,419,429
Trainable params: 6,405
Non-trainable params: 3,413,024
_________________________________________________________________
None
Epoch 1/5


d:\anaconda3\lib\site-packages\keras\optimizer_v2\gradient_descent.py:102: UserWarning: The `lr` argument is deprecated, use `learning_rate` instead.
  super(SGD, self).__init__(name, **kwargs)


103/103 [==============================] - 76s 719ms/step - loss: 0.8647 - accuracy: 0.7782
Epoch 2/5
103/103 [==============================] - 97s 943ms/step - loss: 0.6525 - accuracy: 0.8935
Epoch 3/5
103/103 [==============================] - 92s 896ms/step - loss: 0.6223 - accuracy: 0.9099
Epoch 4/5
103/103 [==============================] - 95s 921ms/step - loss: 0.6021 - accuracy: 0.9226
Epoch 5/5
103/103 [==============================] - 100s 970ms/step - loss: 0.5903 - accuracy: 0.9336

```
第三步：评估模型

```python=
loss, accuracy = model.evaluate(test_data)

```

```python=
12/12 [==============================] - 12s 749ms/step - loss: 0.6107 - accuracy: 0.9155

```

第四步，导出Tensorflow Lite模型

```python=
model.export(export_dir='.')
```
这里导出的Tensorflow Lite模型包含了元数据(metadata),其能够提供标准的模型描述。导出的模型存放在Jupyter Notebook当前的工作目录中。