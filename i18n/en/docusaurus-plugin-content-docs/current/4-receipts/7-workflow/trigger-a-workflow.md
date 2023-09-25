---
sidebar_position: 2
---

# 触发一个工作流

> 谁可以使用这个功能<br />
> 组织管理员、项目管理员和项目成员可触发工作流

## 自动触发的工作流

在项目的记录中，上传一个 Bag 文件。

![upload-bag](../img/upload-bag.png)

该文件将自动触发「生成 ROS bag 索引」工作流。点击【工作流】，查看工作流的运行状态。

![workflow-status](../img/workflow-status.png)

「生成 ROS bag 索引」工作流运行成功后，点击【文件】，查看输出的索引文件。

![view-index](../img/view-index.png)

## 手动触发一个工作流

**在记录详情页触发工作流**

在项目的记录中，上传一个 Bag 文件。

![upload-bag](../img/upload-bag.png)

点击【工作流】，进入工作流分页后，再点击【运行工作流】按钮。

![run-workflow-button](../img/run-workflow-button.png)

跳出「运行工作流」弹框。

<img alt="run-workflow-modal" src={require('../img/run-workflow-modal.png').default} width="500" />

在「运行工作流」弹框中，选择工作流模板。

<img alt="select-workflow-template" src={require('../img/select-workflow-template.png').default} width="500" />

在记录详情页，默认输入记录为当前记录，不可变更。

<img alt="default-record" src={require('../img/default-record.png').default} width="500" />

点击【运行】按钮后，触发工作流。

<img alt="trigger-workflow" src={require('../img/trigger-workflow.png').default} width="500" />
