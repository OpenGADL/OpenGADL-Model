# 实验二 基于LeNet的手写字符图像分类实验

## 1. 实验目的

通过复现经典神经网络LeNet [1]，进一步理解深度学习的工作机制和流程；熟悉神经网络模型的基础结构，对神经网络模型的原理与机制有进一步深入的认识和了解。

## 2. 实验内容

1. 使用OpenGADL Model软件，图形化搭建LeNet模型；

2. 使用OpenGADL Model软件，使用搭建好的LeNet模型在MNIST数据集进行训练和验证。

## 3. 实验步骤

1. 打开OpenGADL Model软件，新建一个项目，命名为LeNetProj；选择任务类型为“图像分类”，并选择项目保存路径；

   ![图1](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251443445.png)

2. 切换到【模型设计】界面，搭建LeNet模型:

   a.【增加可读性，重命名页面名，非必要】新建项目默认添加一个设计页面到设计面板，双击设计页面名，弹出一个命名窗口，重命名设计页面名为LeNet；也可以关闭默认设计页面，新建一个模型设计页面命名为LeNet；

   ![图2](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251443337.png)

   b. 如表1所示，根据LeNet结构，从左侧元件树中选择相应的元件添加到设计页面上;

   |  Input   |       Name       | Kernel | Stride | Padding | Out Channels |
   | :------: | :--------------: | :----: | :----: | :-----: | :----------: |
   | 1×28×28  |      Conv2d      |   5    |   1    |    2    |      6       |
   | 6×28×28  |       Pool       |   2    |   2    |    0    |      6       |
   | 6×14×14  |      Conv2d      |   5    |   1    |    0    |      16      |
   | 16×10×10 |       Pool       |   2    |   2    |    0    |      16      |
   |  16×5×5  |      Conv2d      |   5    |   1    |    0    |     120      |
   |   120    |      Linear      |   -    |   -    |    -    |      84      |
   |    84    |  Linear(Output)  |   -    |   -    |    -    |      10      |
   |    10    | CrossEntropyLoss |   -    |   -    |    -    |      -       |

   **注意：**模型的输入必须是输入元件Input（页面已默认添加），模型的损失函数也应该在设计页面上进行添加（这里使用交叉熵损失函数 CrossEntropyLoss）

   c. 根据LeNet模型的参数对页面上的元件参数进行配置：双击元件，在页面右侧弹出参数配置界面。

   ![图3](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251444117.png)

   **注意：**输入层Input配置输入尺寸用于模型校验，这里LeNet配置的输入尺寸为（1，28，28），对应MNIST数据集的数据尺寸

3. 配置完所有参数后，点击“模型校验”按钮，校验通过后，在模型保存文件夹下生成设计模型对应的代码；

   ![图4_1](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251444874.png)

   ![图4_2](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251444317.png)

4. 切换到【模型训练】界面，进行训练参数的配置：

   a. 选择模型路径：点击打开文件按钮，在弹出的文件对话框中选择当前项目**/project/models/LeNet**； 

   b. 选择数据集：本例使用公开数据集MNIST，点击“使用公开数据集”按钮，在下拉框中选择数据集MNIST；

   c. 选择预训练模型：本例不使用预训练权重，因此点击按钮“不使用预训练模型”；

   d. GPU加速：本例使用单张GPU进行训练，因此点击按钮“使用单个GPU训练”；

   e. 输入尺寸：选择公开数据集的输入尺寸将自动匹配，无需设置；

   f. 训练参数设置界面：配置迭代轮次数为50，批量大小（Batch Size）为8（取决于GPU显存大小）；图像均值和方差由于是公开数据集，已自动配置；优化器选用Adam算法（参数默认）；

   g. 配置完成后，点击“训练”按钮，开始训练；

   训练结束后，在当前项目文件夹**/project/train**得到一个单次训练的文件；

   ![图5](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251445238.png)
   <img src="https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251445390.png" style="zoom:50%;" />
   
   

[1] LECUN Y, BOTTOU L. Gradient-Based Learning Applied to Document Recognition [J]. Proceedings of the IEEE, 1998, 86(11): 2278-2324.

