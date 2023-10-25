# 实验四 基于OpenGADL软件的迁移学习

## 1. 实验目的

通过对自标注数据集进行迁移学习实验，进一步理解深度学习的实际应用；掌握从数据标注到模型选择再到模型训练测试的深度学习全流程工程。

## 2. 实验内容

1. 使用OpenGADL Data软件对提供的猫狗数据集中的**测试集**进行分类任务的数据标注；（训练集和验证集已完成标注）

2. 选用OpenGADL Model提供的预置模型对数据集进行迁移学习；

3. 对拟合后的模型进行测试。

## 3. 实验步骤

示例：使用预置模型Resnet18，在自标注的猫狗数据集进行训练验证和测试。

1. 选择猫狗数据集中的测试集，使用OpenGADL Data软件进行标注；

2. 整理数据集：将训练集train，验证集val以及测试集test按照OpenGADL数据集标准格式进行整理；【**数据集的格式见附录**】

   ![图1](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251449695.png)

3. 打开OpenGADL Model软件，新建一个项目，命名为Resnet18DogCat；选择任务类型为“图像分类”，并且选择项目保存路径

   ![图2](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251449350.png)

4. 切换界面到【模型训练】，进行配置：

   a. 选择模型路径：选择预置模型的情况下，模型文件夹不需要选择，由软件自动生成；

   b. 选择数据集：本例使用自标注的猫狗数据集DogCat；点击“使用用户数据集”按钮，点击打开文件按钮，选择数据集路径；软件将通过这个路径去自动匹配目录下的train和val数据集；

   c. 使用预训练模型：本例使用软件预置模型，因此点击按钮“使用系统提供的预训练模型”，下拉框中依次选择“resnet”，“18”；

   d. GPU加速：本例使用单张GPU进行训练，因此点击按钮“使用单个GPU训练”；

   e. 输入尺寸：根据数据集图片大小，选择一个合适的大小224×224；

   f. 训练参数设置界面：配置迭代轮次数为20，批量大小（Batch Size）为64（取决于GPU显存大小）；图像均值和方差全设为0交由软件根据数据集自动计算；优化器Optimizer选用Adam算法（参数默认）；

   ![图3](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251449718.png)

   g. 配置完成后，点击“训练”按钮，开始训练；

   h. 训练结束后，在当前项目文件夹/project/train得到一个单次训练的文件；

   ![图4_1](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251450561.png)

   ![图4_2](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251450788.png)

   ![图4_3](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251450910.png)

5. 切换界面到【评估部署】，进行配置：

   a. 选择模型：选择要进行测试的模型文件夹；软件自动会生成预置模型的模型文件夹，存放在当前项目文件夹**/project/models/**下

   b. 选择权重文件：软件会自动加载模型文件夹下的**.pkl/.pth**文件，选择刚刚训练好的权重文件；

   c. 选择数据：本例使用自标注的数据集，因此点击按钮“选择数据集”，选择猫狗数据集的路径；

   d. GPU加速：本例使用单张GPU进行测试，因此点击按钮“使用单个GPU测试”；

   e. 测试参数配置界面：输入尺寸，图像均值，图像方差应该与训练界面的参数一致，才能得到正确的测试结果；【软件在训练后默认自动将测试界面的这几个参数与训练界面的这几个参数进行同步】；

   ![图5](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251451345.png)

   f. 配置完成，点击“测试”，开始测试；

   g. 测试结束后，将以表格形式显示测试结果，并在下方显示数据集的测试报告。

   ![图6_1](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251451495.png)

   ![图6_2](https://raw.githubusercontent.com/OpenGADL/OpenGADL-Model/main/picture/202310251451301.png)

   



# 附录

OpenGADL数据集标准格式：

		- 目标检测数据集文件夹
			- annotation	
				-- picture_1.json
				-- picture_2.json
				……
			- config
				-- categories.txt
				-- test.txt
				-- train.txt
				-- val.txt
			- images.txt
			- project_info.json

1. 划分为三个部分，分别为标签文件夹**“annotations”**，配置文件夹**“config”**以及保存所有数据集图片路径的**“image.txt”**文件。

2. annotations文件夹中存放了所有图片的标签json文件，包括训练集train、验证集val和测试集test。【测试集的标签json文件需要手动添加，如图所示，将在GADL_Data中完成标注后的测试集标签文件添加到标准数据集中】

   ![图7](https://raw.githubusercontent.com/MagnetoXxz/My_pictures/main/Test_picture/202310251452074.png)

3. config文件夹中存放了**categories.txt、test.txt、train.txt和val.txt**文件。其中categories.txt文件存储标签类别与id的映射字典，如图所示：

   ![图8](https://raw.githubusercontent.com/MagnetoXxz/My_pictures/main/Test_picture/202310251452348.png)

   【注意：标签类别id必须从0开始】test.txt、train.txt和val.txt文件分别存储了测试集、训练集和验证集的图片路径。【**存储的图片路径为绝对路径，图片所在位置一旦改变了，相应的路径需要修改！！！**】

4. image.txt文件存储了该数据集中所有图片的绝对路径，如图所示。【**存储的图片路径为绝对路径，图片所在位置一旦改变了，相应的路径需要修改！！！**】

   ![图9](https://raw.githubusercontent.com/MagnetoXxz/My_pictures/main/Test_picture/202310251452512.png)

