# sppnet

### 摘要

论文开篇提出现有的CNN算法要求输入是一个固定大小(fixed-size)的图片，这一限定是“刻意”(artificial)的，并且可能会影响算法在检测不同大小图片上的精度。空间金字塔池化(spatial pyramid pooling)可以解决这一问题。同时SPPnet在多个数据集上(ImageNet2012, Pascal VOC 2007,…)表现优异。

### 解决的问题

之前的许多CNN图像识别算法要求固定大小的图像作为输入，而对于不满足要求的图像，要先采用预处理的方式使其符合要求。

RCNN在检测精度上表现良好，但是计算开销过大。

![图像预处理](sppnet%209bfdb274fd8a4af885f491cf1d0479f3/Untitled.png)

图像预处理

### 方法

传统的CNN方法要求固定大小的输入，这是因为最后的全连接层要求固定大小的输入。从这个思路入手，作者提出，对于图像大小的限制“只在网络的深层”出现，进而可以通过在全连接层之前加入spp层来加以满足。

![传统方法（上）与SPPnet（下）](sppnet%209bfdb274fd8a4af885f491cf1d0479f3/Untitled%201.png)

传统方法（上）与SPPnet（下）

作者指出，SPP（更多地以spatial pyramid matching, SPM为人所知，~~所以是Kaiming为了体现创新之处还改了个名？233~~）是CV领域最成功的方法之一，但是从未被考虑过与CNN放在一起。

接下来，作者提出：因为卷积层并不关心输入层的大小，并且卷积的结果可以提取出特定的语义信息，可以考虑在最后加入一个pooling层，将这些语义信息提取为一个定长的张量喂给最后的全连接层。

![spp层图例，通过等比例的池化层获得定长的张量。](sppnet%209bfdb274fd8a4af885f491cf1d0479f3/Untitled%202.png)

spp层图例，通过等比例的池化层获得定长的张量。

### 效果展示

- 总之效果非常好。一句话概括：和之前计算开销小的算法比效果好，和之前效果好的算法（RCNN）比计算开销小。

![Untitled](sppnet%209bfdb274fd8a4af885f491cf1d0479f3/Untitled%203.png)

![Untitled](sppnet%209bfdb274fd8a4af885f491cf1d0479f3/Untitled%204.png)

### 问题与展望