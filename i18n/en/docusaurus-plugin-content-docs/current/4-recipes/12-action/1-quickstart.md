---
sidebar_position: 1
---

# Quick Start

Quickly create and execute automation tasks in the coScene system.

## Introduction

This tutorial will guide you through creating an action and setting up a trigger in the coScene system, which automatically executes when a `finish.flag` file is uploaded.

## Getting Started

### 1. Create an Action

Follow these steps to create an action:

![create action](../img/action-create-action.png)

- Name the action `coscene-test`.
- Add a tag `hello`.
- Use `busybox:latest` as the image.
- Set the command `ls -al $(COS_FILE_VOLUME)` to list all files.
- Leave environment variables empty.
- Set compute resources to `1 core/2G`.

### 2. Create a Trigger

![create trigger](../img/action-create-trigger.png)

- Name the trigger.
- Link it to the `coscene-test` action.
- Set the file wildcard to `finish.flag`, which triggers the action when a file with this name is uploaded.
- Leave other conditions empty for now.

After setting up, create the trigger.

### 3. Create a Record and Upload a File

![create record](../img/action-create-record.png)

Create a new record and upload a file named `finish.flag`.

### 4. View Invocations

After the file is upload, the system will check the trigger and execute the related action. View the action's execution details in the invocation list.

![action runs](../img/action-runs.png)

Click to view the detailed information.

![action run detail](../img/action-run-detail.png)

On the detail page, review the logs to confirm the action's execution and the files listed.

## Next Steps

You have successfully created and tested an automation process. For a more detailed understanding, please refer to further documentation.
