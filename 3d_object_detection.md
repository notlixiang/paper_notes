<!--
 * @Date: 2022-01-09 11:17:34
 * @LastEditTime: 2022-01-12 22:21:18
 * @LastEditors: Li Xiang
 * @Description: 
 * @FilePath: \paper_notes\3d_object_detection.md
-->

# 3D目标物检测

- [3D目标物检测](#3d目标物检测)
  - [DETR3D](#detr3d)
  - [FCOS3D](#fcos3d)

## DETR3D

DETR3D: 3D Object Detection from Multi-view Images via 3D-to-2D Queries

[[abstract](https://arxiv.org/abs/2110.06922)]
[[pdf](https://arxiv.org/pdf/2104.10956)]
[[code](https://github.com/WangYueFt/detr3d)]

将DETR思想扩展到多相机视觉3D目标物检测任务，生成bev中的检测结果。

使用query产生object proposal，并转换为BEV中的3D point，再投影到像素坐标系中用以关联图像特征。

在nuscenes数据集上超过FCOS3D，达到sota。

![](images/2022-01-09-12-45-38.png)

## FCOS3D

FCOS3D: Fully Convolutional One-Stage Monocular 3D Object Detection

[[abstract](https://arxiv.org/abs/2104.10956)]
[[pdf](https://arxiv.org/pdf/2104.10956)]
[[code](https://github.com/open-mmlab/mmdetection3d/blob/master/configs/fcos3d/README.md)]

相比2D目标检测的FCOS，改用基于高斯分布的Centerness生成机制。

在位置检测头部分，每个像素上预测目标物3D中心点在图像中投影的相对位置，目标物中心到相机距离，目标物长宽高，旋转角，速度。

最终在Nuscenes上整体精度超过CenterNet，但未给出推理时间。

![](images/2022-01-12-22-12-17.png)

![](images/2022-01-12-22-13-57.png)

![](images/2022-01-12-22-21-52.png)