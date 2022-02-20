<!--
 * @Date: 2022-01-09 11:17:34
 * @LastEditTime: 2022-02-20 14:31:36
 * @LastEditors: Li Xiang
 * @Description: 
 * @FilePath: \paper_notes\2d_object_detection.md
-->
# 2D目标物检测与图片分类

- [2D目标物检测与图片分类](#2d目标物检测与图片分类)
  - [CenterNet](#centernet)
  - [FCOS](#fcos)
  - [Deformable-DETR](#deformable-detr)


## CenterNet

Objects as Points

[[abstract](https://arxiv.org/abs/1904.07850)]
[[pdf](https://arxiv.org/pdf/1904.07850)]
[[code](https://github.com/xingyizhou/CenterNet)]

一种无锚的目标物检测头设计，在heatmap上回归出有目标物中心点落在各个像素上的置信度，通过heatmap上的局部极大值生成proposal，从而不需要对检测框做NMS后处理。

相比MaskRCNN，YOLOv3等算法，该方法在精度与速度上取得较好的均衡，并可扩充到人体姿态估计，自动驾驶的3D目标物检测等任务上。

对于目标物中心点重叠，进而导致该方法失效的场景，经过统计，在COCO数据集中的出现概率小于0.1%，影响很轻微。

![](images/2022-01-10-22-15-10.png)

![](images/2022-01-10-22-35-38.png)

![](images/2022-01-10-22-22-13.png)

## FCOS

FCOS: Fully Convolutional One-Stage Object Detection

[[abstract](https://arxiv.org/abs/1904.01355)]
[[pdf](https://arxiv.org/pdf/1904.01355)]
[[code](https://github.com/tianzhi0549/FCOS)]

提出一种无锚的目标物检测头，在不同尺度的特征图中，每个像素生成到当前目标物所在检测框上下左右四边的距离(t,b,l,r)来给出proposal。

除此之外，每个像素也回归到对应bbox的中心度，用来滤除离目标物中心距离过远的像素生成的低质量box。

在coco数据集上的精度超过Faster R-CNN与RetinaNet等众多两阶段与单阶段检测算法，推理速度领先 Faster R-CNN 约20%。

![](images/2022-01-09-21-11-31.png)

![](images/2022-01-09-21-05-21.png)


## Deformable-DETR

Deformable DETR: Deformable Transformers for End-to-End Object Detection

[[abstract](https://arxiv.org/abs/2010.04159)]
[[pdf](https://arxiv.org/pdf/2010.04159)]
[[code](https://github.com/fundamentalvision/Deformable-DETR)]

一种基于DETR的目标物检测方法，有效提高ViT支撑的特征图分辨率，并提高训练效率。

相比原版DETR中每个query对特征图各像素都做cross-attention，Deformable-DETR的query生成若干采样位置，并从特征图中通过双线性插值离散的抽取特征，并持续调整采样点。

方法很新颖，但计算效率及精度相比SOTA并未有较大提升，主要优点还是在于训练时间上；而且离散采样存在大量的随机内存访问，对于嵌入式平台的部署可能不友好。

![](images/2022-02-20-14-14-17.png)

![](images/2022-02-20-14-18-21.png)

![](images/2022-02-20-14-28-48.png)