---
sidebar_position: 1
---

# 快速入门

学习如何在刻行系统中快速创建和执行自动化。

## 介绍

本文指导你创建一个动作，用以列举特定记录下所有文件，并设置触发器，在上传 `finish.flag` 文件时自动触发该动作。

## 开始

### 1. 创建动作

按照以下步骤创建动作：

![create action](../img/action-create-action.png)

- 命名动作为 `coscene-test`。
- 标签使用 `hello`。
- 镜像选择 `busybox:latest`。
- 命令设置为 `ls -al $(COS_FILE_VOLUME)`，列举数据目录下所有文件。
- 环境变量留空。
- 计算要求选择最小配置 `1核/2G`。

### 2. 创建触发器

![create trigger](../img/action-create-trigger.png)

- 名称自定义。
- 关联到 `coscene-test` 动作。
- 文件通配符设置为 `finish.flag`。
- 条件留空。

完成后，点击创建触发器。

### 3. 创建记录并上传文件

![create record](../img/action-create-record.png)

创建新记录并上传名为 `finish.flag` 的文件。

### 4. 查看调用历史

上传 `finish.flag` 后，系统将验证触发器条件并执行动作。在调用历史中可以查看到执行记录。

![action runs](../img/action-runs.png)

点击查看详情。

![action run detail](../img/action-run-detail.png)

查看日志确认 `ls -al $(COS_FILE_VOLUME)` 命令执行情况和列出的文件。

## 下一步

你已完成自动化流程的创建和执行，继续阅读文档以深入了解其他功能。
