---
sidebar_position: 3
---

# Workflow Parameters

CoScene's workflows support passing parameters at runtime as inputs to the workflow. These parameters can be used throughout the runtime lifecycle of the workflow.

This chapter takes the user-triggered **"Generate ROS bag Index"** workflow as an example to show how to customize input parameter values. After the workflow completes, the input parameters can be seen on the workflow details page.

## Input Parameters

In records with Bag files, go to the "Workflow" tab.

![view-workflow](../img/view-workflow.png)

In the list of all workflows on the left, click on &#8203;`oaicite:{"number":1,"invalid_reason":"Malformed citation 【Timeline Alignment】"}`&#8203;.

<img alt="select-align-timeline-template" src={require('../img/select-align-timeline-template.png').default} width="600" />

On the "Timeline Alignment" workflow page, click the &#8203;`oaicite:{"number":2,"invalid_reason":"Malformed citation 【Run Workflow】"}`&#8203; button.

<img alt="workflow-parameter-run-button" src={require('../img/workflow-parameter-run-button.png').default} width="600" />

The "Run Workflow" pop-up appears, where you can customize the values of input parameters. These include:

- **compression**: The compression method used for the output package, default is "lz4".
- **interval**: Frame interval, default is "50ms".
- **topic**: The topic to be extracted for alignment, by default all topics are extracted.

<img alt="input-workflow-parameters" src={require('../img/input-workflow-parameters.png').default} width="500" />

After editing the input parameters as needed, click the &#8203;`oaicite:{"number":3,"invalid_reason":"Malformed citation 【Run】"}`&#8203; button to trigger the workflow.

<img alt="edit-workflow-parameters" src={require('../img/edit-workflow-parameters.png').default} width="500" />

## View Parameters

On the "Workflow" tab of the record details page, go to the "Timeline Alignment" workflow page. Click the name of the workflow you want to view to go to the workflow details page.

![view-parameters-list](../img/view-parameters-list.png)

On the workflow details page, view the input parameters used when running the workflow.

![view-workflow-parameter](../img/view-workflow-parameter.png)
