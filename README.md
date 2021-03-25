# License-Plate-Recognition

原是《视听觉信号处理》视觉部分的实验三，当时完成匆促，仅仅使用了基本的图像形态学变换对车牌的形状进行检测。对实验进行了完善，由于尚未系统的学习深度学习相关的知识，因此此处的深度学习训练结果使用开源识别系统[EasyPR](https://github.com/liuruoze/EasyPR)。

基于opencv3实现的车牌识别，包括算法和客户端界面，[surface.py](./surface.py)是界面代码，[predict.py](./predict.py)是算法代码。

## 使用方法：
版本：python3.7.4，opencv3.4和numpy1.14和PIL5<br>
下载源码，并安装python、numpy、opencv的python版、PIL，运行surface.py即可。

## 算法实现：
算法思想来自于网上资源，先使用图像边缘和车牌颜色定位车牌，再识别字符。车牌定位在predict方法中。车牌字符识别也在predict方法中，请参看源码中的注释，需要说明的是，车牌字符识别使用的算法是opencv的SVM， opencv的SVM使用代码来自于opencv附带的sample，StatModel类和SVM类都是sample中的代码。SVM训练使用的训练样本来自于github上的[EasyPR](https://github.com/liuruoze/EasyPR)的c++版本。由于训练样本有限，测试时会发现，车牌字符识别可能存在误差，尤其是第一个中文字符出现的误差概率较大。源码中，附带了[EasyPR](https://github.com/liuruoze/EasyPR)中的训练样本，在[train/](./train/)目录下，如果要重新训练请解压在当前目录下，并删除原始训练数据文件svm.dat和svmchinese.dat。

**额外说明**：算法识别准确性依赖[EasyPR](https://github.com/liuruoze/EasyPR)的训练情况，测试中发现，车牌定位算法的参数受图像分辨率、色偏、车距影响（test目录下的车牌的像素都比较小，其他图片很可能因为像素等问题识别不了，识别其他像素的车牌需要修改config文件里面的参数）。
