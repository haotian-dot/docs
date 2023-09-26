---
sidebar_position: 2
---

# Trigger a Workflow

> Who can use this feature<br />
> Organization administrators, project administrators, and project members can trigger workflows

## Automatically Triggered Workflow

In the project records, upload a Bag file.

![upload-bag](../img/upload-bag.png)

This file will automatically trigger the "Generate ROS bag index" workflow. Click on the &#8203;`oaicite:{"number":1,"invalid_reason":"Malformed citation 【Workflow】"}`&#8203; to check the running status of the workflow.

![workflow-status](../img/workflow-status.png)

After the "Generate ROS bag index" workflow runs successfully, click on &#8203;`oaicite:{"number":2,"invalid_reason":"Malformed citation 【Files】"}`&#8203; to view the output index file.

![view-index](../img/view-index.png)

## Manually Trigger a Workflow

**Trigger a workflow from the record details page**

In the project records, upload a Bag file.

![upload-bag](../img/upload-bag.png)

Click on &#8203;`oaicite:{"number":3,"invalid_reason":"Malformed citation 【Workflow】"}`&#8203;, enter the workflow page, and then click on the &#8203;`oaicite:{"number":4,"invalid_reason":"Malformed citation 【Run Workflow】"}`&#8203; button.

![run-workflow-button](../img/run-workflow-button.png)

A "Run Workflow" modal will pop up.

<img alt="run-workflow-modal" src={require('../img/run-workflow-modal.png').default} width="500" />

In the "Run Workflow" modal, select the workflow template.

<img alt="select-workflow-template" src={require('../img/select-workflow-template.png').default} width="500" />

On the record details page, the default input record is the current record and cannot be changed.

<img alt="default-record" src={require('../img/default-record.png').default} width="500" />

After clicking the &#8203;`oaicite:{"number":5,"invalid_reason":"Malformed citation 【Run】"}`&#8203; button, the workflow will be triggered.

<img alt="trigger-workflow" src={require('../img/trigger-workflow.png').default} width="500" />
