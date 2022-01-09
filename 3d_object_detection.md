<!--
 * @Date: 2022-01-09 11:17:34
 * @LastEditTime: 2022-01-09 12:52:47
 * @LastEditors: Li Xiang
 * @Description: 
 * @FilePath: \paper_notes\3d_object_detection.md
-->

# 3D目标物检测

## DETR3D

DETR3D: 3D Object Detection from Multi-view Images via 3D-to-2D Queries

[[paper](https://arxiv.org/abs/2110.06922)]
[[pdf](https://arxiv.org/pdf/2104.10956)]
[[code](https://github.com/WangYueFt/detr3d)]

![](images/2022-01-09-12-45-38.png)

将DETR思想扩展到3D多相机视觉目标物检测任务。使用query产生object proposal，并转换为BEV中的3D point，再投影到像素坐标系中用以关联图像特征。最终生成bev中的检测结果。

## FCOS3D

FCOS3D: Fully Convolutional One-Stage Monocular 3D Object Detection

[[paper](https://arxiv.org/abs/2104.10956)]
[[pdf](https://arxiv.org/pdf/2104.10956)]
[[code](https://github.com/open-mmlab/mmdetection3d/blob/master/configs/fcos3d/README.md)]
