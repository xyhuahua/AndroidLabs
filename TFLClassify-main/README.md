# 基于TensorFlow Lite实现的Android花卉识别应用
# 下载初始代码

创建工作目录，使用

```powershell
git clone https://github.com/hoitab/TFLClassify.git

```

拷贝代码；或者直接访问github链接下载代码的ZIP包，并解压缩到工作目录。
在Android studio打开下载好的代码，下载好需要的依赖包后，连接到真实的手机运行。

![](https://markdown.liuchengtu.com/work/uploads/upload_690c538afd13956e0f4d7c33494aac09.jpg)

之后打开New>Other>TensorFlow Lite Model

![](https://markdown.liuchengtu.com/work/uploads/upload_ea069f1905b492cc1a900118e94b8f61.png)

选择finish模块中ml文件下的FlowerModel.tflite。

![](https://markdown.liuchengtu.com/work/uploads/upload_88223c70f5febcfae78f53914ac490b5.png)

之后成功导入

![](https://markdown.liuchengtu.com/work/uploads/upload_7b66d10f40a348542c056db8abd78840.png)

打开TODO窗口

![](https://markdown.liuchengtu.com/work/uploads/upload_963b3394403e2499d66e1b599e92b32f.png)

之后呈现如下窗口：
![](https://markdown.liuchengtu.com/work/uploads/upload_6630ba9f1cc7a81fe29abca1b58ae74b.png)

# 添加代码重新运行APP
在TODO1后面添加如下代码：
```kotlin
// TODO 1: Add class variable TensorFlow Lite Model  private  val flowerModel = FlowerModel.newInstance(ctx)
```

在TODO2后面添加如下代码：
```kotlin
// TODO 2: Convert Image to Bitmap then to TensorImage  val tfImage = TensorImage.fromBitmap(toBitmap(imageProxy))
```

在TODO3后面添加如下代码：
```kotlin
 val outputs = flowerModel.process(tfImage)  .probabilityAsCategoryList.apply  { sortByDescending 
     { it.score } }.take(MAX_RESULT_DISPLAY) 
```

在TODO4后面添加如下代码：
```kotlin
// TODO 4: Converting the top probability items into a list of recognitions  
for  (output in outputs)  { 
    items.add(Recognition(output.label, output.score)) 
}
```

将原先用于虚拟显示识别结果的代码注释掉或者删除

```kotlin
// START - Placeholder code at the start of the codelab. Comment this block of code out.
for (i in 0..MAX_RESULT_DISPLAY-1){
    items.add(Recognition("Fake label $i", Random.nextFloat()))
}
// END - Placeholder code at the start of the codelab. Comment this block of code out.

```
连接到手机再次运行
结果如下：

![](https://markdown.liuchengtu.com/work/uploads/upload_1258fc8ec61e68c69f53df3a8a9fdadc.jpg)


![](https://markdown.liuchengtu.com/work/uploads/upload_f9af3f6d5cadf135cc40e0e833912583.jpg)
