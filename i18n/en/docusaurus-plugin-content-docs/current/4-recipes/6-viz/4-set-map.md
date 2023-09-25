---
sidebar_position: 4
---

# View and Configure Map Data

本章节将介绍如何进行地图 topic 的查看与设置。

## 查看/隐藏地图 topic

### 查看/隐藏地图 topic

### 查看视图中某点对应 topic 的信息

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/3D-view-point-information.mp4" controls="controls" width="700" height="400"></video>

## 设置地图属性

### 调整地图透明度

若地图被覆盖（未显示地图），可调整最上层地图的透明度，以调整电梯地图透明度为例：

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/3D-setting-map-transparency.mp4" controls="controls" width="700" height="400"></video>

### 调整地图边界

若地图未显示边界，可关闭 move_base/global_costmap/costmap。

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/3D-setting-map-boundary.mp4" controls="controls" width="700" height="400"></video>

## 导入地图

当播放的 bag 中需要使用地图时，可导入机器的地图文件 map.png 和 map.yaml，以在可视化页面中使用该地图。

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/import-map.mp4" controls="controls" width="700" height="400"></video>

### 提取地图

coScene 支持从 bag（包含 map topic ）中自动提取地图，以便作为共享数据在同一项目中使用该地图。

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/extract-map.mp4" controls="controls" width="700" height="400"></video>

### 复制地图

当查看 bag 分析问题需要地图数据时，可从已提取出地图的记录中，将地图文件复制到当前记录。

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/copy-map.mp4" controls="controls" width="700" height="400"></video>

### 设置导入的地图属性

外部导入的地图 topic 默认为关闭状态，需要设置对应的属性才能正确展示在可视化中。

<video src="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/viz/setting-out-map.mp4" controls="controls" width="700" height="400"></video>

根据导入的地图背景颜色建议以下示例参数：

- 地图背景偏向于蓝白色
  - Color mode：Gradient
  - Gradient：左侧 #0011ffff，右侧 #ffffffff
  - Value min：-20
  - Value max：1
- 地图背景偏向于灰黑色
  - Color mode：Gradient
  - Gradient：左侧 #e5e5e5ff，右侧 #000000ff
  - Value min：-2
  - Value max：0
