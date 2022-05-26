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


```python
image_path = tf.keras.utils.get_file(
      'flower_photos.tgz',
      'https://storage.googleapis.com/download.tensorflow.org/example_images/flower_photos.tgz',
      extract=True)
image_path = os.path.join(os.path.dirname(image_path), 'flower_photos')

```


```python
from tflite_model_maker.image_classifier import DataLoader
data = DataLoader.from_folder(image_path)
train_data, test_data = data.split(0.9)

```

    INFO:tensorflow:Load image with size: 3670, num_label: 5, labels: daisy, dandelion, roses, sunflowers, tulips.
    

    INFO:tensorflow:Load image with size: 3670, num_label: 5, labels: daisy, dandelion, roses, sunflowers, tulips.
    


```python
model = image_classifier.create(train_data)
```

    INFO:tensorflow:Retraining the models...
    

    INFO:tensorflow:Retraining the models...
    

    Model: "sequential_1"
    _________________________________________________________________
     Layer (type)                Output Shape              Param #   
    =================================================================
     hub_keras_layer_v1v2_1 (Hub  (None, 1280)             3413024   
     KerasLayerV1V2)                                                 
                                                                     
     dropout_1 (Dropout)         (None, 1280)              0         
                                                                     
     dense_1 (Dense)             (None, 5)                 6405      
                                                                     
    =================================================================
    Total params: 3,419,429
    Trainable params: 6,405
    Non-trainable params: 3,413,024
    _________________________________________________________________
    None
    Epoch 1/5
    103/103 [==============================] - 72s 677ms/step - loss: 0.8687 - accuracy: 0.7667
    Epoch 2/5
    103/103 [==============================] - 76s 736ms/step - loss: 0.6593 - accuracy: 0.8990
    Epoch 3/5
    103/103 [==============================] - 74s 720ms/step - loss: 0.6234 - accuracy: 0.9147
    Epoch 4/5
    103/103 [==============================] - 75s 727ms/step - loss: 0.5992 - accuracy: 0.9281
    Epoch 5/5
    103/103 [==============================] - 78s 752ms/step - loss: 0.5803 - accuracy: 0.9369
    


```python
loss, accuracy = model.evaluate(test_data)
```

    12/12 [==============================] - 10s 631ms/step - loss: 0.6259 - accuracy: 0.9046
    


```python
model.export(export_dir='.')
```

    INFO:tensorflow:Assets written to: C:\Users\xiaolei\AppData\Local\Temp\tmp2zxq7zli\assets
    

    INFO:tensorflow:Assets written to: C:\Users\xiaolei\AppData\Local\Temp\tmp2zxq7zli\assets
    c:\python39\lib\site-packages\tensorflow\lite\python\convert.py:766: UserWarning: Statistics for quantized inputs were expected, but not specified; continuing anyway.
      warnings.warn("Statistics for quantized inputs were expected, but not "
    
