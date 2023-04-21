# 构建第一个Kotlin应用
## 打开Android studio，创建新项目，选择Basic Activity
![](https://huatu.98youxi.com/markdown/work/uploads/upload_f2b559c16aad9af2f8c6fc28a7051827.png)
## 配置
### 点击右上角的手机图案，之后点击Create Physical
![](https://huatu.98youxi.com/markdown/work/uploads/upload_2053893ea60da0ff303784652e4ed773.png)
### 选择一部手机后点击下一步，等待安装
![](https://huatu.98youxi.com/markdown/work/uploads/upload_be5b11eee551a28811c788e41089ced3.png)
### 运行查看效果
![](https://huatu.98youxi.com/markdown/work/uploads/upload_582281b70c0b7ae72c197f77eb18a4a9.png)
## 第一个项目
### 1、添加一个按钮
①找到fragment_first.xml文件，点击右上角的Split，再点击左边的Palette 
![](https://huatu.98youxi.com/markdown/work/uploads/upload_ab9480f8088845cb6413575c7f1661a9.png)
②用鼠标把Button拖入到应用界面中。
### 2、设置按钮的约束
①设置Button的Top>BottonOf textView
```xml
app:layout_constraintTop_toBottomOf="@+id/textview_first" />
```
②随后添加Button的左侧约束至屏幕的左侧，Button的底部约束至屏幕的底部。查看Attributes面板，修改将id从button修改为toast_button（注意修改id将重构代码）
③点击Extract string resource
![](https://huatu.98youxi.com/markdown/work/uploads/upload_49e1c66d49e6955b07edc4875f2c3cf2.png)
④弹出对话框，令资源名为toast_button_text，资源值为Toast，并点击OK
![](https://huatu.98youxi.com/markdown/work/uploads/upload_2a74c9bfd495f7439a74a72e547fe452.png)

### 3、调整Next 按钮
①在设计视图右键相应约束，选择Delete，也可以在属性面板的Constraint Widget中移动光标到相应约束点击删除，之后添加Next的右边和底部约束至父类屏幕（如果不存在的话），Next的Top约束至TextView的底部。最后，TextView的底部约束至屏幕的底部。
②更新Next的名字，为random_button
### 4再添加一个按钮
向fragment_first.xml文件中添加第三个按钮，位于Toast和Random按钮之间，TextView的下方。新Button的左右约束分别约束至Toast和Random，Top约束至TextView的底部，Buttom约束至屏幕的底部
![](https://huatu.98youxi.com/markdown/work/uploads/upload_1b16b1c9ea4e8805691753a4b9fd6d8b.png)
### 5、设置外观
在values>colors.xml定义了一些应用程序可以使用的颜色
![](https://huatu.98youxi.com/markdown/work/uploads/upload_5a8858d816120cabe1c1ad8ddf494b6e.png)
添加新颜色screenBackground 值为 #2196F3，这是蓝色阴影色；添加新颜色buttonBackground 值为 #BBDEFB

```xml
<color name="screenBackground">#2196F3</color>
<color name="buttonBackground">#BBDEFB</color>
```
之后 fragment_first.xml的属性面板中设置屏幕背景色为
![](https://huatu.98youxi.com/markdown/work/uploads/upload_7f950c1a34b6c88a15bb91a4f0be137e.png)
2、 设置每个按钮的背景色为**buttonBackground**
```xml
android:background="@color/buttonBackground"
```
![](https://huatu.98youxi.com/markdown/work/uploads/upload_c36526a424b476c48168070b0da94dcb.png)
还需要修改需修改res/values/themes.xml的style值，添加**.Bridge**。
![](https://huatu.98youxi.com/markdown/work/uploads/upload_6ea2586f675aaed9767a6c6dbc1a95f5.png)
3、移除TextView的背景颜色，设置TextView的文本颜色为color/white，并增大字体大小至72sp
```xml
        android:textColor="@android:color/white"
        android:textSize="72sp"
```
### 设置布局
Toast与屏幕的左边距设置为24dp，Random与屏幕的右边距设置为24dp，利用属性面板的Constraint Widget完成设置。
![](https://huatu.98youxi.com/markdown/work/uploads/upload_02eaee9143914b3616e69568f44e6362.png)
设置TextView的垂直偏移为0.3
![](https://huatu.98youxi.com/markdown/work/uploads/upload_d1b0f8303f8fa9a8f7633a7968393eb3.png)
### 最后结果
![](https://huatu.98youxi.com/markdown/work/uploads/upload_56350d6f437ff6700f27ee0a003be19a.png)

###  添加代码完成应用程序交互
![](https://huatu.98youxi.com/markdown/work/uploads/upload_4fc3bb64df69c2c2f5a468d6e1e5ded5.png)

在FirstFragment.kt文件的onViewCreated函数改为
```xml
  override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)

        binding.randomButton.setOnClickListener {
            findNavController().navigate(R.id.action_FirstFragment_to_SecondFragment)
        }
        // find the toast_button by its ID and set a click listener
        view.findViewById<Button>(R.id.toast_button).setOnClickListener {
            // create a Toast with some text, to appear for a short time
            val myToast = Toast.makeText(context, "Hello Toast!", Toast.LENGTH_LONG)
            // show the Toast
            myToast.show()
        }


        view.findViewById<Button>(R.id.count_button).setOnClickListener {
            countMe(view)
        }

    }
```

### 第二个节目的代码

①去掉TextView和Button之间的约束
②拖动新的TextView至屏幕的中间位置，用来显示随机数
③设置新的TextView的id为**@+id/textview_random**
④设置新的TextView的左右约束至屏幕的左右侧，Top约束至⑤textview_second的Bottom，Bottom约束至Button的Top
⑥设置TextView的字体颜色textColor属性为**@android:color/white**，textSize为72sp，textStyle为bold
⑦设置TextView的显示文字为“R”
⑧设置垂直偏移量layout_constraintVertical_bias为0.45

```xml
<TextView  
android:id="@+id/textview_random"  
android:layout_width="wrap_content"  
android:layout_height="wrap_content"  
android:text="R"  
android:textColor="@android:color/white"  
android:textSize="72sp"  
android:textStyle="bold"  
app:layout_constraintBottom_toTopOf="@+id![] 
app:layout_constraintEnd_toEndOf="parent"  
app:layout_constraintStart_toStartOf="parent"  
app:layout_constraintTop_toBottomOf="@+id/textview_header"  
app:layout_constraintVertical_bias="0.45" />
```

#### 更新显示界面文本的TextView(textview_second)
代码如下
```xml
    <TextView
        android:id="@+id/textview_header"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="24dp"
        android:layout_marginLeft="24dp"
        android:layout_marginTop="24dp"
        android:layout_marginEnd="24dp"
        android:layout_marginRight="24dp"
        android:text="@string/random_heading"
        android:textColor="@color/colorPrimaryDark"
        android:textSize="24sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
```

#### 更改界面的背景色和按钮布局
① 向colors.xml文件添加第二个Fragment背景色的值，修改fragment_second.xml背景色的属性为`screenBackground2`
```xml
<color name="screenBackground2">#26C6DA</color>
```
![](https://huatu.98youxi.com/markdown/work/uploads/upload_d948c4bb797c7ad170477bea948c8744.png)

### 导航
打开nav_graph.xml文件（**res>navigation>nav_graph.xml**）
![](https://huatu.98youxi.com/markdown/work/uploads/upload_b3480fcbaf2a31d0453537f6147405c7.png)

## 启用SafeArgs

[SafeArgs](https://developer.android.com/guide/navigation/navigation-pass-data)是一个 gradle 插件，它可以帮助您在导航图中输入需要传递的数据信息，作用类似于Activity之间传递数据的Bundle。
Gradle的Project部分，在plugins节添加
```xml
id 'androidx.navigation.safeargs.kotlin' version '2.5.0-alpha01' apply false
```

module部分在plugins节添加
```xml
id 'androidx.navigation.safeargs'
```


#### 创建导航动作的参数
打开导航视图，点击FirstFragment，查看其属性。
在Actions栏中可以看到导航至SecondFragment
同理，查看SecondFragment的属性栏
点击Arguments **+**符号
弹出的对话框中，添加参数myArg，类型为整型Integer
![](https://huatu.98youxi.com/markdown/work/uploads/upload_4b84bf26def283d3eafcc0695019424d.png)

#### FirstFragment添加代码，向SecondFragment发数据
```xml
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)

        binding.randomButton.setOnClickListener {
            val showCountTextView = view.findViewById<TextView>(R.id.textview_first)
            val currentCount = showCountTextView.text.toString().toInt()
            val action = FirstFragmentDirections.actionFirstFragmentToSecondFragment(currentCount)
            findNavController().navigate(action)
//            findNavController().navigate(R.id.action_FirstFragment_to_SecondFragment)
        }
        // find the toast_button by its ID and set a click listener
        view.findViewById<Button>(R.id.toast_button).setOnClickListener {
            // create a Toast with some text, to appear for a short time
            val myToast = Toast.makeText(context, "Hello Toast!", Toast.LENGTH_LONG)
            // show the Toast
            myToast.show()
        }


        view.findViewById<Button>(R.id.count_button).setOnClickListener {
            countMe(view)
        }

    }
```
### 更新SecondFragment.kt的代码，接受传递过来的整型参数并进行处理
1. 导入navArgs包

```kotlin
import androidx.navigation.fragment.navArgs
```
2. 修改onViewCreated
```Kotlin
override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)

        val count = args.myArg
        val countText = getString(R.string.random_heading, count)
        view.findViewById<TextView>(R.id.textview_header).text = countText
        val random = java.util.Random()
        var randomNumber = 0
        if (count > 0) {
            randomNumber = random.nextInt(count + 1)
        }
        view.findViewById<TextView>(R.id.textview_random).text = randomNumber.toString()

        binding.buttonSecond.setOnClickListener {
            findNavController().navigate(R.id.action_SecondFragment_to_FirstFragment)
        }
    }
```

### 最后运行程序
①点击Toast按钮，会有消息弹出

![](https://huatu.98youxi.com/markdown/work/uploads/upload_6b26041457da931c93a5aac27aba7bed.png)

②不断点击COUNT按钮，数字会加一显示在屏幕上

![](https://huatu.98youxi.com/markdown/work/uploads/upload_ffbcfb70ea696305fe793fb955297161.png)

③点击RANDOM按钮，跳转到第二个页面，并且显示0-18中的一个随机数。

![](https://huatu.98youxi.com/markdown/work/uploads/upload_62842aa0a5aea4763a7e7361bf9bd10e.png)



