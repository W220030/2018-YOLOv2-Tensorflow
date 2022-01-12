运行环境：
Python3 + Tensorflow1.5 + OpenCV-python3.3.1 + Numpy1.13
windows和ubuntu环境都可以


准备工作：
请在yolo2检测模型下载模型，并放到yolo2_model文件夹下


文件说明：
1、model_darknet19.py：yolo2网络模型——darknet19
2、decode.py：解码darknet19网络得到的参数
3、utils.py：功能函数，包含：预处理输入图片、筛选边界框NMS、绘制筛选后的边界框
4、config.py：配置文件，包含anchor尺寸、coco数据集的80个classes类别名称
5、Main.py：YOLO_v2主函数，对应程序有三个步骤：
（1）输入图片进入darknet19网络得到特征图，并进行解码得到：xmin xmax表示的边界框、置信度、类别概率
（2）筛选解码后的回归边界框——NMS
（3）绘制筛选后的边界框
6、Loss.py：Yolo_v2 Loss损失函数（train时候用，预测时候没有调用此程序）
（1）IOU值最大的那个anchor与ground truth匹配，对应的预测框用来预测这个ground truth:计算xywh、置信度c(目标值为1)、类别概率p误差。
（2）IOU小于某阈值的anchor对应的预测框：只计算置信度c(目标值为0)误差。
（3）剩下IOU大于某阈值但不是max的anchor对应的预测框：丢弃，不计算任何误差。
7、yolo2_data文件夹：包含待检测输入图片car.jpg、检测后的输出图片detection.jpg、coco数据集80个类别名称coco_classes.txt
