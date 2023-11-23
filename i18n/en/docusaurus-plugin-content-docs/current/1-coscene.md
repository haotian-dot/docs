---
sidebar_position: 1
id: intro
---

# Overview

Welcome to the coScene platform. coScene is an operational and development platform based on scene data, helping businesses and users manage complex device and behavior data. In today's era of explosive growth in multimodal data, coScene provides an open, instantly available, cloud-native, and neutral solution.

## Feature Overview

### Scene Data Management and Visualization

Scene data is large in size, difficult to understand in its raw form, complex in format, and lacks a unified standard. The sources of this data are varied, making it challenging and high-threshold to handle. Addressing these challenges, coScene offers a complete set of scene data management and usage solutions. Users can efficiently utilize scene data through APIs, web applications, and desktop software.

### Customize Your Workflow

With coScene's workflow engine, you can conveniently build large-scale workflow applications on scene data without worrying about data preparation and computing resource scheduling. In the workflow template management page, you can find workflow templates created by team members and also discover various data processing workflow templates provided officially by coScene.

### Semantic Search Engine

The coScene semantic search engine provides an open framework for search and discovery. Users can build their own scene classification libraries and corresponding indexes on coScene, allowing for rapid retrieval and discovery of scene data. This is particularly useful in managing multimodal scene data. For example, in autonomous driving, users can quickly find a specific traffic sign through the search engine, or in robotics, quickly discover a specific object.

## System Concepts

Upon logging into coScene, you can immediately use all the official features of the platform. Here are some introductions to the main concepts.

### Organization

Users from the same company, organization, or group will be assigned to the same organization. The organization's administrators can set different permissions for different users to precisely control data access.

### Project

A project is the smallest unit of permission management in coScene. Users can manage the visibility of data using projects. Whether you want to share all the data of a project within the organization or keep the data of a project still in development confidential, projects can be used for logical segmentation. Records, moments, and other data within a project belong to the project and inherit its visibility within the organization.

### Record

The record is a core concept of coScene, encompassing all the data that users want to aggregate together. A single ROS Bag might not represent the full picture of a test, often requiring additional files like configuration files, map files, and test reports.

### Moment

A record might be a long data segment, like a complete autonomous driving session from start to finish. Within this, there may be many interesting data points, such as a lane change or an emergency evasion. These interesting data points are the most quality segments within the vast data. coScene provides the Moment model for users to mark and manage such time points, facilitating better discovery and utilization of high-quality data segments in subsequent data processing.

Refer to our quick start guide to learn more about coScene's features.
