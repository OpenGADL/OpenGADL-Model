# 实验三 基于OpenGADL软件的模型设计

## 1. 实验目的

通过自主复现/设计常见的神经网络模型，进一步加深对神经网络模型原理的理解。通过对神经网络超参数的配置，熟悉神经网络模型调优过程，进一步巩固深度学习的基础知识。

## 2. 实验内容

1. 使用OpenGADL Model软件，复现经典分类神经网络模型ResNet18；
2. 使用OpenGADL Model软件，在相应的公开数据集上训练验证搭建好的ResNet18模型。

## 3. 实验步骤

示例：复现一个ResNet18 [2]模型，在公开数据集CIFAR10进行训练和验证：

1. 打开OpenGADL Model软件，新建一个项目，命名为“ResNetCifar10”；选择任务类型为“图像分类”，并选择项目保存路径；

   ![图1](https://raw.githubusercontent.com/MagnetoXxz/My_pictures/main/Test_picture/202310251446564.png)

2. 切换到【模型设计】界面，搭建ResNet18模型：

   a.【增加可读性，重命名页面名，非必要】新建项目默认添加一个设计页面到设计面板，双击设计页面名，弹出一个命名窗口，重命名设计页面名为resnet18；也可以关闭默认设计页面，新建一个模型设计页面命名为resnet18； 

   b. 根据ResNet18结构，从左侧元件树中选择相应的元件添加到设计页面上。为了使整个网络的结构化更加清晰，这里根据文章[2]中的结构进行了宏模块抽取（ResNet18网络结构详见附录）；

   **注意：**模型的输入必须是输入元件Input（页面已默认添加），模型的损失函数也应该在设计页面上进行添加（这里使用交叉熵损失函数 CrossEntropyLoss）；

   c. 根据ResNet18模型的参数对页面上的元件参数进行配置：双击元件，在页面右侧弹出参数配置界面。

   ![图2_1](https://raw.githubusercontent.com/MagnetoXxz/My_pictures/main/Test_picture/202310251446798.png)

   ![图2_2](https://raw.githubusercontent.com/MagnetoXxz/My_pictures/main/Test_picture/202310251446322.png)

3. 配置完所有参数后，点击“模型校验”按钮，校验通过后，在模型保存文件夹下生成设计模型对应的代码；

4. 切换到【模型训练】界面，进行训练参数的配置：

   a. 选择模型路径：点击打开文件按钮，在弹出的文件对话框中选择当前项目**/project/models/resnet18**；

   b. 选择数据集：本例使用公开数据集CIFAR10；点击“使用公开数据集”按钮，在下拉框中选择数据集CIFAR10；

   c. 选择预训练模型：本例不使用预训练权重，因此点击按钮“不使用预训练模型”；

   d. GPU加速：本例使用单张GPU进行训练，因此点击按钮“使用单个GPU训练”；

   e. 输入尺寸：选择公开数据集的输入尺寸将自动匹配，无需设置；

   f. 训练参数设置界面：配置迭代轮次数为50，批量大小（Batch Size）为8（取决于GPU显存大小）；图像均值和方差由于是公开数据集，已自动配置；优化器选用Adam算法（参数默认）；

   g. 配置完成后，点击“训练”按钮，开始训练；

   h. 训练结束后，在当前项目文件夹**/project/train**得到一个单次训练的文件。

   ![图3](https://raw.githubusercontent.com/MagnetoXxz/My_pictures/main/Test_picture/202310251447145.png)



[2] He K, Zhang X, Ren S, et al. Deep residual learning for image recognition[C]// Proceedings of the IEEE conference on computer vision and pattern recognition. 2016: 770-778.











# 附录

<center>表1 ResNet18网络结构</center>

|   Input   |  Layer   |       Name       | Kernel | Stride | Padding | Out Channles |
| :-------: | :------: | :--------------: | :----: | :----: | :-----: | :----------: |
|  3×32×32  |   Conv   |      Conv2d      |   3    |   1    |    1    |      64      |
| 64×32×32  | Block1_1 |      Conv2d      |   3    |   1    |    1    |      64      |
|           |          |      Conv2d      |   3    |   1    |    1    |      64      |
| 64×32×32  | Block1_2 |      Conv2d      |   3    |   1    |    1    |      64      |
|           |          |      Conv2d      |   3    |   1    |    1    |      64      |
| 64×32×32  | Block2_1 |    Conv2d_1×1    |   1    |   2    |    0    |     128      |
|           |          |      Conv2d      |   3    |   2    |    1    |     128      |
|           |          |      Conv2d      |   3    |   1    |    1    |     128      |
| 128×16×16 | Block1_3 |      Conv2d      |   3    |   1    |    1    |     128      |
|           |          |      Conv2d      |   3    |   1    |    1    |     128      |
| 128×16×16 | Block2_2 |    Conv2d_1×1    |   1    |   2    |    0    |     256      |
|           |          |      Conv2d      |   3    |   2    |    1    |     256      |
|           |          |      Conv2d      |   3    |   1    |    1    |     256      |
|  256×8×8  | Block1_4 |      Conv2d      |   3    |   1    |    1    |     256      |
|           |          |      Conv2d      |   3    |   1    |    1    |     256      |
|  256×8×8  | Block2_3 |    Conv2d_1×1    |   1    |   2    |    0    |     512      |
|           |          |      Conv2d      |   3    |   2    |    1    |     512      |
|           |          |      Conv2d      |   3    |   1    |    1    |     512      |
|  512×4×4  | Block1_5 |      Conv2d      |   3    |   1    |    1    |     512      |
|           |          |      Conv2d      |   3    |   1    |    1    |     512      |
|  512×4×4  |   Pool   |    AvgPool2d     |   4    |   1    |    0    |     512      |
|    512    |  OutPut  |      Linear      |   -    |   -    |    -    |      10      |
|    10     |   Loss   | CrossEntropyLoss |   -    |   -    |    -    |      -       |

表1为ResNet18网络中使用模块的表格，其中Block n_m 指第n类Block，使用了m次，Conv2d_1×1指卷积核为1×1的卷积。本实验使用的ResNet18中，Block的种类共两种：Block1和Block2，两种Block的具体结构如下图所示：

![图4_1](https://raw.githubusercontent.com/MagnetoXxz/My_pictures/main/Test_picture/202310251448761.png)

![图4_2](https://raw.githubusercontent.com/MagnetoXxz/My_pictures/main/Test_picture/202310251448934.png)

**注意**：与Block1相比，Block2中多使用了一个卷积操作：Conv2d_1×1。