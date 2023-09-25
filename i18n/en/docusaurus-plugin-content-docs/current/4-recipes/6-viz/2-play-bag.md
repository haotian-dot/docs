---
sidebar_position: 2
---

# Replay a ROS Bag

可视化界面按 bag 文件的时间顺序，播放整条记录。本章节将介绍如何播放记录中的 bag，以及播放相关的设置。

## 播放 bag

> 记录中的 bag 处理成功后，即可进行播放。

在可视化界面，点击「播放」图标开始播放 bag。

若记录中有多个 bag，则可切换播放：点击左侧「数据源」-「播放列表」，选择目标 bag 即跳转到对应时间开始播放。

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/play-viz-and-playlist.mp4" controls="controls" width="700" height="400"></video>

**循环播放与倍速播放**

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/loop-play-and-speed.mp4" controls="controls" width="700" height="400"></video>

**跳帧播放**

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/seek-forward.mp4" controls="controls" width="700" height="400"></video>

## 查看时间轴详情

> 展示当前播放的时间，以及标记的时间段。

黑色竖线表示当前播放时间，橙色竖线表示光标在时间轴上移动时对应的时间，蓝色线段表示标记 (即「一刻」) 的时间，紫色区域表示记录中所有可播 bag 文件。

<img alt="honeybee-6" src={require('../img/honeybee-6.png').default} width="1200" />

<br />

## 切换播放视角

可视化界面支持多角度查看 bag 中的可视化内容。

### 回到画面中心

在播放过程中，可使用按钮或滚轮调整画面大小，或一键回到预设的画面中心。

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/recenter.mp4" controls="controls" width="700" height="400"></video>

### 切换 2D/3D 视角

在 3D 视角下，通过【ctrl】+ 鼠标左键即可 360° 旋转查看视图；在 2D 视角下，可在俯视视角下旋转查看视图。

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/3d-and-zoom.mp4" controls="controls" width="700" height="400"></video>

<br />

## 查看当前视图中每个颜色对应的 topic

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/3D-view-point-information.mp4" controls="controls" width="700" height="400"></video>
