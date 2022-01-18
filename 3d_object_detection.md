<!--
 * @Date: 2022-01-09 11:17:34
 * @LastEditTime: 2022-01-18 21:56:38
 * @LastEditors: Li Xiang
 * @Description: 
 * @FilePath: \paper_notes\3d_object_detection.md
-->

# 3D目标物检测

- [3D目标物检测](#3d目标物检测)
  - [DETR3D](#detr3d)
  - [FCOS3D](#fcos3d)
  - [Pseudo-LiDAR](#pseudo-lidar)
  - [OFT](#oft)
  - [ImVoxelNet](#imvoxelnet)
  - [FISHING Net](#fishing-net)
  - [BEVDet](#bevdet)

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

## Pseudo-LiDAR

Pseudo-LiDAR from Visual Depth Estimation: Bridging the Gap in 3D Object Detection for Autonomous Driving

[[abstract](https://arxiv.org/abs/1812.07179)]
[[pdf](https://arxiv.org/pdf/1812.07179)]
[[code](https://github.com/mileyan/pseudo_lidar)]

认为深度图这种数据表示形式影响了3D目标检测的位置精度。

将单目深度估计或双目相机的结果转换为点云形式，称为伪激光雷达，再利用点云目标检测算法进行处理。

在具体实现中，也进行了2D-3D数据的融合(F-PointNet, AVOD)，精度得到了提高。

![](images/2022-01-15-21-18-25.png)

![](images/2022-01-15-21-17-43.png)

## OFT

Orthographic Feature Transform for Monocular 3D Object Detection

[[abstract](https://arxiv.org/abs/1811.08188)]
[[pdf](https://arxiv.org/pdf/1811.08188)]
[[code](https://github.com/tom-roddick/oft)]

提出一种图片特征转BEV的方法。

将空间分为voxel，通过相机内外参计算每个voxel在图片中的投影，将覆盖的区域的2D特征求和作为voxel的特征，最终在BEV中进行目标检测。

在KITTI 3D Object Detection中达到SOTA。

![](images/2022-01-15-21-23-15.png)

![](images/2022-01-15-21-19-58.png)

![](images/2022-01-15-21-25-54.png)

## ImVoxelNet
ImVoxelNet: Image to Voxels Projection for Monocular and Multi-View General-Purpose 3D Object Detection

[[abstract](https://arxiv.org/abs/2106.01178)]
[[pdf](https://arxiv.org/pdf/2106.01178)]
[[code](https://github.com/saic-vul/imvoxelnet)]

多相机版本的OFT。

BEV检测部分取消掉了Top-Down Network，改用3D Conv，从而理论上可以分辨Z方向的物体。

(论文结果展示中的室内部分都只有地面目标物，略迷惑)

![](images/2022-01-16-20-29-05.png)

![](images/2022-01-16-20-33-33.png)

![](images/2022-01-16-20-34-22.png)

## FISHING Net
FISHING Net: Future Inference of Semantic Heatmaps In Grids

[[abstract](https://arxiv.org/abs/2006.09917)]
[[pdf](https://arxiv.org/pdf/2006.09917)]
[code]

将多模态数据都在BEV中进行表示，再对BEV特征张量进行融合，融合方法可选pooling或基于softmax的类别优先。

将固定时间间隔的多帧进行输入，并预测固定时间间隔后的多帧结果。

相比对于所有特征拼接后做TOP-DOWN的卷积，这种融合方式可以使用同一个网络融合不同的传感器配置，具有较好的拓展性。

![](images/2022-01-17-21-50-21.png)

![](images/2022-01-17-21-56-23.png)

## BEVDet

BEVDet: High-performance Multi-camera 3D Object Detection in Bird-Eye-View

[[abstract](https://arxiv.org/abs/2112.11790)]
[[pdf](https://arxiv.org/pdf/2112.11790)]
[[code](https://github.com/HuangJunJie2017/BEVDet)]

总结了一种多目相机BEV感知的范式，用于工程中模块化网络设计，并提供了数据增强策略。

将网络分成了图片特征编码，IMG2BEV转换，BEV编码，检测头四个部分，并给出了一些选型。

在未提出新的模型结构的前提下，做出了nuscenes上的SOTA结果，具备较大的工程参考意义。

(Github上只有个结果图，没放代码，看样子够呛能开源)

![](images/2022-01-18-21-51-44.png)

![](images/2022-01-18-21-53-06.png)

![](images/2022-01-18-21-54-24.png)