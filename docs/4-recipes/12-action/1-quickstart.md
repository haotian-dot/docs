---
sidebar_position: 1
---

# 快速入门

快速在刻行系统中创建和执行自动化任务。

## 介绍

本教程将指导您如何在刻行系统中创建一个动作以及设置触发器，以实现在上传 `finish.flag` 文件时自动执行动作。

## 开始

### 1. 创建动作

遵循以下步骤创建一个动作：

![create action](../img/action-create-action.png)

- 动作命名为 `coscene-test`。
- 添加标签 `hello`。
- 使用 `busybox:latest` 作为镜像。
- 设置命令 `ls -al $(COS_FILE_VOLUME)`，以列举所有文件。
- 环境变量留空。
- 计算资源设置为 `1核/2G`。

### 2. 创建触发器

![create trigger](../img/action-create-trigger.png)

- 为触发器命名。
- 关联至 `coscene-test` 动作。
- 文件通配符设为 `finish.flag`，当有此文件名的文件上传时，触发动作。
- 其他条件可暂留空。

完成设置后创建触发器。

### 3. 创建记录并上传文件

![create record](../img/action-create-record.png)

新建记录并上传名为 `finish.flag` 的文件。

### 4. 查看调用历史

文件上传后，系统将检查触发器并执行相关动作。在调用历史中查看动作的执行情况。

![action runs](../img/action-runs.png)

点击进入查看详细信息。

![action run detail](../img/action-run-detail.png)

在详情页面，查看日志以确认动作执行的结果和列出的文件。

## 下一步

您已成功创建并测试了一个自动化流程。若需更详细了解，请参阅相关文档。
