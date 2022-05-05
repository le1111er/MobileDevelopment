# Project3

## 1.导入项目

从github上下载项目的zip，等待gradle sync。如果出现Sync failed，查阅idea.log。我的问题是sdk版本不匹配，添加android-29即可。

## 2.寻找TODO并添加代码

``` kotlin
 // TODO 1: Add class variable TensorFlow Lite Model
        // Initializing the flowerModel by lazy so that it runs in the same thread when the process
        // method is called.

        private val flowerModel = FlowerModel.newInstance(ctx) // 使用参数为ctx的构造方法构造FlowerModel对象
```

``` kotlin
// TODO 2: Convert Image to Bitmap then to TensorImage
            val tfImage = TensorImage.fromBitmap(toBitmap(imageProxy))
	// 转换图片为Bitmap再转换为TensorImage
```

``` kotlin
// TODO 3: Process the image using the trained model, sort and pick out the top results
            val outputs = flowerModel.process(tfImage)
                .probabilityAsCategoryList.apply {
                    sortByDescending { it.score }
                }.take(MAX_RESULT_DISPLAY) // 获取相似度ouputs，并按照降序排序，取相似度最高的为结果
```

``` kotlin
// TODO 4: Converting the top probability items into a list of recognitions
            for(output in outputs) {
                items.add(Recognition(output.label, output.score))
            } // 输出相似度最高的三个的标签和相似度
```

## 3.运行结果

![Screenshot_2022-05-05-16-01-56-274_org.tensorflow.lite.examples.classification](\Project3.assets\Screenshot_2022-05-05-16-01-56-274_org.tensorflow.lite.examples.classification-16517378583211.jpg)