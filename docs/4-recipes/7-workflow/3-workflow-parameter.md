---
sidebar_position: 3
---

# 工作流参数

刻行的工作流支持运行时传入参数作为工作流的输入，这些参数在整个工作流的运行生命周期中都可以被使用。

本章节以用户触发**「提取静态 TF」**这个工作流为例，展示自定义输入参数的值。当工作流运行完成后，在工作流详情页面能看到输入的参数。

## 输入参数

在有 Bag 文件的记录中，进入「工作流」分页。

![record-wf](../img/record-wf.png)

在左侧全部工作流列中，点击【提取静态 TF】。

![record-wf-tf](../img/record-wf-tf.png)

在「提取静态 TF」的工作流页面，点击【运行工作流】按钮。

![record-wf-tf-run](../img/record-wf-tf-run.png)

跳出「运行工作流」弹框，可自定义输入参数的值。其中：

- **filename**： 为需要提取静态 TF 的文件名称。

  ![input-workflow-parameters](../img/input-workflow-parameters.png)

点击【运行】按钮，触发工作流。

## 查看参数

在记录详情页的「工作流」分页，进入「提取静态 TF」的工作流页面。点击待查看工作流的名称，进入工作流详情页。

![view-wk-tf-list](../img/view-wk-tf-list.png)

在工作流详情页，查看运行工作流时的输入参数。

![view-workflow-parameter](../img/view-workflow-parameter.png)
