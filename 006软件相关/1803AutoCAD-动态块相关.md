## 动态块相关

基本逻辑：先参数后动作。

### 01. 动态块双向拉伸

目前找到了 2 种实现方案。（2021-05-26）

#### 1.1 线性参数居中方案

[第04课 CAD 基础拉伸动态块制作-双向拉伸](https://www.bilibili.com/video/av71869013/)

1、加线性参数，两端各做一个拉伸动作。

2、线性参数，「其他」面板里把基点位置设置为「中点」。

#### 1.2 拉伸方向相反方案

1、加线性参数，两端各做一个拉伸动作。

2、以垂直方向的螺栓动态块为例。两个拉伸动作里，「替代」面板里，角度偏移原来的值都是「90」，因为是往下拉伸。两个拉伸动作肯定是 180 度的反向，接着把上面的拉伸动作的角度偏移更改为「-90」，系统会自动变成 270。

[了解动态块，大虫老师教你所有的动态块制作方法](https://www.bilibili.com/video/BV1a7411V75v/?spm_id_from=333.788.b_7265636f5f6c697374.15)

目前方案 2 没实现，原因待研究。（2021-05-26）
