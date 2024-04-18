---
sidebar_position: 1
---

# About Cloud Test

Batch testing aims to meet users' needs for large-scale testing in a productized manner, with application scenarios including regression testing, simulation testing, etc.

Users can upload and manage relevant images, test data, test suites, and test packages on the coScene platform, run batch tests within the project scope, monitor progress, and obtain test results.

<br />

## Basic Concepts

| Concept Name       | Description                                                                                                                                  |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Configuration File | A file written by the user specifying the parameters required for batch test execution. It is uploaded or edited online before testing.      |
| Image              | The virtual environment for running batch tests. Users push images to the platform and specify the image version during testing.             |
| Test Suite         | Typically a set of tests for similar scenarios, executed in batch during batch testing. Users upload test suites using a configuration file. |
| Test Bundle        | Typically a series of codes and related dependencies written for executing test cases. Users upload test bundles to manage its versions.     |
| Test Case          | The specific task executed during the batch test, usually parsed from the corresponding test report.                                         |

<br />

## Overview of the Usage Process

Click to enter the project's "Batch Testing" page and create a batch test according to the page prompts:

![regression](../img/regression.png)

The following step-by-step overview provides you with a basic process for using the batch testing feature:

1. Upload test data to the coScene project and store it as a record.
2. Ensure the organization has the appropriate available image or push images to the coScene platform.
3. Upload or edit the configuration file online on the "Test Suite Management" page to obtain the test suite and corresponding configuration parameters.
4. Upload the test package file on the "Test Package Management" page to generate a test package version; if the uploaded test package meets the test suite association trigger condition, it will automatically trigger a batch test.
5. On the "Batch Testing" page, click the button and select run parameters (test package version, test suite, etc.) to run the batch test; or run the batch test directly from the command line locally.
6. Click on the batch test to view the progress and test results.

For more detailed steps, please refer to the detailed explanations in the following chapters.

<br />
