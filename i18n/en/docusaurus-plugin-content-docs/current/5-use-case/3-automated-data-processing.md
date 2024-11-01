---
sidebar_position: 3
---

# Automated Data Processing

While the AI era brings unprecedented opportunities through vast amounts of data, it also presents significant challenges in data management and processing. AI engineers regularly perform repetitive tasks like data cleaning, preprocessing, training, testing, and deployment - all of which require substantial time and resources. The coScene platform's automation system eliminates this manual overhead by allowing users to configure data processing workflows once and reuse them automatically, improving both efficiency and accuracy while reducing human error.

This guide demonstrates automated data processing using a practical example: automatically extracting image frames from uploaded MP4 video files.

## Prerequisites

Before starting, ensure you have:

- Docker installed and running on your local machine
- Access to the coScene platform
- Basic familiarity with Python and Docker concepts

## Project Overview

This automation workflow consists of three main components:

1. A Docker container that processes video files
2. An automated action in coScene that runs the container
3. A trigger that executes the action when MP4 files are uploaded

## Preparing Image Files

We'll create two key files that define our video processing container:

1. A Dockerfile that sets up the environment
2. A Python script that handles the frame extraction

## Accessing the Image Registry

To store and manage our Docker image, we'll use coScene's built-in image registry. Follow these steps to set up registry access:

## Building and Pushing the Image

After preparing the image files and configuring registry access, we'll build the container and make it available in coScene:

## Configuring Automation

The automation setup consists of two parts:

1. Creating an action that defines what to run
2. Setting up a trigger that determines when to run it

## Testing the Workflow

To verify the automation:

1. Create a new record in your project
2. Upload an MP4 file (sample provided)
3. Monitor the automatic processing
4. Review the extracted frames

## Summary

You've now set up an automated workflow that:

- Monitors for new MP4 file uploads
- Automatically processes videos to extract frames
- Saves the results for further use

This example demonstrates just one possibility of coScene's automation capabilities. For more advanced use cases and features, explore the following resources:

- [Automation Documentation](https://docs.coscene.cn/docs/category/%E8%87%AA%E5%8A%A8%E5%8C%96/)
- [Image Registry Guide](https://docs.coscene.cn/docs/category/%E9%95%9C%E5%83%8F/)
