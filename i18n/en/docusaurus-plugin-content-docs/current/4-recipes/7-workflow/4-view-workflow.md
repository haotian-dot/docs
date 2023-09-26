---
sidebar_position: 4
---

# List Running Workflows

Once a workflow is triggered, a workflow execution task is created. After the workflow starts running, you can see a list of running progress and view the logs and basic information of each step on coScene.

## Workflow List

In the "Workflow List", all workflows in the project are displayed, allowing you to easily view the results of workflow execution.

Click on "Workflow" in the left sidebar of the project to access the project's workflow page.

<img alt="goto-workflow" src={require('../img/goto-workflow.png').default} width="180" />

The left list displays the types of workflow templates. Click on the template type you want to view to expand the corresponding workflow list.

![workflow-template](../img/workflow-template.png)

The workflow list displays the workflow status, name, initiator, trigger time, and duration.

![list-workflow](../img/list-workflow.png)

## Workflow Details

In "Workflow Details", detailed information of a single workflow is displayed, providing a comprehensive overview of the workflow's execution results.

Select the workflow you want to view, click on "Workflow Name" to enter the workflow details page. The workflow details page is divided into four parts: **Basic Information, Step Logs and Information, Inputs, and Outputs**.

![goto-workflow-detail](../img/goto-workflow-detail.png)

### Basic Information

The top of the workflow details page displays basic information, including workflow status, initiator, trigger time, duration, and input parameters.

![workflow-base-info](../img/workflow-base-info.png)

### Step Logs and Information

Once the workflow has finished running, the "Steps" tab of the workflow will list the execution steps of the workflow.

![goto-step](../img/goto-step.png)

Click on the step you want to view to display the workflow log for that step.

![click-stepname](../img/click-stepname.png)

In the workflow log search box, enter keywords to highlight the search results.

<img alt="search-log" src={require('../img/search-log.png').default} width="700" />

Click on "Basic Information" to view the main details of the step, including its name, ID, status, etc.

![workflow-step-detail](../img/workflow-step-detail.png)

### Inputs & Outputs

**Switch to the "Input Record Version" tab of the workflow.**

- The input record name and version are displayed. Click on the "Record Name" to jump to that record; click on the "Version Link" to jump to the corresponding record version.

  ![input-record-info](../img/input-record-info.png)

- The list below displays information about the files included in the records input to the workflow.

  ![input-record-file](../img/input-record-file.png)

**Switch to the "Outputs" tab of the workflow.**

- The output information is displayed.

  ![workflow-output](../img/workflow-output.png)
