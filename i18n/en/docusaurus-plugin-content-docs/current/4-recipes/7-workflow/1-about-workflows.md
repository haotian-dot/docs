---
sidebar_position: 1
---

# About Workflow

A workflow is a configurable automated process that runs one or more jobs. By configuring [system events](../../3-concepts/1-data-models.md#system-events) and workflow templates, workflows can be automatically triggered when specific events occur. Workflows can also be manually triggered at any time.

## Basic Elements of a Workflow

A workflow consists of the following basic elements:

- Triggers: One or more events that trigger the workflow, or it can be manually triggered by users.
- One or more steps (step), each of which will be executed on the platform's computing node, with logs, artifacts, and results recorded separately.
- Each step can run predefined scripts, programs, or packaged container images. These executable units often contain repeatable user and business logic and can be reused extensively.

## Workflow Templates

Apart from allowing users to define their templates, CoScene is continuously adding various practical basic workflow templates. Currently, CoScene has predefined three workflow templates, with each template capable of performing different tasks.

The predefined workflow templates are: Generate ROS bag index, timeline alignment, and export records to OSS.

### Generate ROS bag Index

- Generate an index for the Bag file to achieve faster loading speeds when playing the file in the visualization page. "According to CoScene tests: Files with an index in the visualization page have a loading speed 10+ times faster than files without an index."
- Trigger Method: Automatically triggered after uploading a Bag file or manually triggered.

### Timeline Alignment

- Align the timeline of Topics in the Bag file.

- Trigger Method: Manually triggered.

### Export Records to OSS

- Import files from records into OSS.

- Trigger Method: Manually triggered.
