<!--
 * @Date: 2022-01-23 12:05:34
 * @LastEditTime: 2022-01-23 17:32:08
 * @LastEditors: Li Xiang
 * @Description: 
 * @FilePath: \paper_notes\backbones.md
-->

# 网络主干

- [网络主干](#网络主干)
  - [ShuffleNet V2](#shufflenet-v2)
  - [ResNet 数学推导](#resnet-数学推导)
  - [ResNeXt](#resnext)
  - [Rethinking ImageNet Pre-training](#rethinking-imagenet-pre-training)

## ShuffleNet V2

ShuffleNet V2: Practical Guidelines for Efficient CNN Architecture Design

[[abstract](https://arxiv.org/abs/1807.11164)]
[[pdf](https://arxiv.org/pdf/1807.11164)]
[[code](https://github.com/pytorch/vision/blob/5a315453da/torchvision/models/shufflenetv2.py)]

文章指出，FLOPS并不能完全衡量网络推理速度，数据IO时的内存访问成本(MAC, Memory Access Cost)也很影响推理效率。

基于对MAC的分析，提出四个设计高效CNN的实用指导规则：卷积层相等的输入输出通道数量能最小化内存访问成本(卷积尽量不变换通道数)，组卷积分组过多会增加内存访问成本(合理分组卷积)，网络碎片化会降低并行度(网络分支别太多)，逐元素(relu,add,bias等)操作FLOP低却带来大量内存访问成本(规避element wise操作)。

在以上规则指导下，通过通道分离只对一半的通道做卷积，再和未卷积的另一半concat后做channel shuffle，设计了新的网络结构，有准又快。

![](images/2022-01-11-22-50-44.png)


## ResNet 数学推导

Identity Mappings in Deep Residual Networks

[[abstract](https://arxiv.org/abs/1603.05027)]
[[pdf](https://arxiv.org/pdf/1603.05027)]
[[code](https://github.com/KaimingHe/resnet-1k-layers)]

通过ResNet中网络层梯度的数学推导，说明ResNet易于训练的原因是恒等映射使得其梯度中存在一项1，使得训练时的梯度能够直接传达到任意一层。

通过设计不同shortcut的对比实验，证明了数学推导的有效性。

另外，对ResNet中Conv,BN,Act层的排布顺序进行了探索与优化，提出了更优的pre-activation结构。

(经典作品，数学推导很漂亮，必须精度的论文)

![](images/2022-01-20-22-04-08.png)

![](images/2022-01-20-22-05-35.png)

![](images/2022-01-20-22-08-49.png)

## ResNeXt

Aggregated Residual Transformations for Deep Neural Networks

[[abstract](https://arxiv.org/abs/1611.05431)]
[[pdf](https://arxiv.org/pdf/1611.05431)]
[[code](https://github.com/facebookresearch/ResNeXt)]

在ResNet基础上，提出block内部并行的模块数量(称为cardinality)，也是模型一个重要维度，并设计了新的综合了ResNet和Inception的网络结构，称为ResNeXt。

本质上是将三层卷积的ResBlock中的中间一层换成了分组卷积，用以降低参数和计算量。

(故事讲得很好，也确实有提升，但感觉主要是GroupConv的功劳，命名为ResNeXt略微牵强)

![](images/2022-01-23-17-32-44.png)

![](images/2022-01-23-17-25-32.png)

## Rethinking ImageNet Pre-training

Rethinking ImageNet Pre-training

[[abstract](https://arxiv.org/abs/1811.08883)]
[[pdf](https://arxiv.org/pdf/1811.08883)]
[code]

研究了ImageNet预训练的作用，指出预训练权重在训练早期能加快模型收敛，但在有充足训练数据的前提下，预训练模型并不能提高最终的精度。

在训练数据不足时，预训练模型仍有很大意义。

(数据是深度学习的基础)


![](images/2022-01-13-22-35-23.png)

