---
sidebar_position: 9
---

# Configuration Yaml Example

> Through this section, you can understand the writing rules of batch testing configuration files; this section will also provide sample files for reference.

<br />

Supported configuration files are of the type yaml or yml, and the name must be **cos.yaml** or **cos.yml**. You can copy directly or <a href="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/regression/cos.yaml.zip" download>click here to download</a> the sample configuration file and make modifications. Its basic structure is as follows:

## Customize Testing Suite {#customize-testing-bundle}

Set the test suite name, test type, and the command used to run the test.

```yaml
version: '1'
jobs:
  - name: 'Test Positioning Issue-1'
    type: 'generic'
    images:
      base: cr.coscene.cn/coscene-hello/position:v1.0.0
    parameters:
      script:
        - /bin/sh
        - -c
        - 'echo hello'
```

- **name: Test Suite Name**

  Custom test suite name displayed on the web interface.

- **type: Test Type**

  Currently supported test types are: "generic" and "gazebo".

- **images - base: Image Address**

  The image serves as the virtual environment for running batch tests. You need to specify the image version address in the configuration file for each test suite to use when running.

- **parameters - scripts: Running Parameters**

  Used to specify the command each test suite runs.

<br />

## Define Multiple Test Suites {#define-multiple-jobs}

A batch test consists of one or more test suites, which can run in parallel.

```yaml
version: '1'
jobs:
  - name: 'Test Positioning Issue-1'

  - name: 'Test Positioning Issue-2'
```

<br />

## Use Labels to Call Records {#query-records-by-labels}

Set the labels used for associated records: Each test case will use its associated record as test data, and the associated record will be the record that matches the conditions of the labels.

```yaml
records:
  labels:
    - 'Positioning Issue'
```

- **records - labels: Corresponding record labels**

  Writing rules for the labels section are as follows:

  - Logical Operators

    - Supports and only supports three logical operators: `AND`, `OR`, and `NOT`. All operators must be in uppercase.
    - Parentheses `(` `)` can be used to clarify the priority of operators. Note that `OR` has a higher priority, i.e., `a AND b OR c` is equivalent to `a AND (b OR c)`.

    - After `NOT` can only be a label, not an expression, while after `AND` and `OR` can be either a label or an expression.

      For example, `NOT a` is valid, but `NOT (a AND b)` is invalid (it can be rewritten as `NOT a OR NOT b`).

    - The relationship between labels on multiple lines is equivalent to `OR`.

  - Spaces

    - `AND` and `OR` must each have a space before and after; `NOT` must have a space after it.
    - Labels cannot contain spaces.

  - Others

    - Labels cannot contain substrings of `AND`, `OR`, or `NOT`. For example, `label_NO` is an invalid label.

    - Labels cannot contain parentheses `(` `)`. For example, `(label` is an invalid label.

    - Pure numeric labels must be enclosed in quotes `'`.

<br />

## Specify Resource Size {#specify-resources}

By default, batch tests provide a resource size of 1 core and 2 GB. You can manually specify the size in the parameter list.

```yaml
parameters:
  resource: small  # 1C2G

parameters:
  resource: medium # 2C4G

parameters:
  resource: large  # 4C8G

parameters:
  resource: xlarge # 8C16G
```

<br />

## Auto-Triggering Tests {#auto-triggering}

Set the conditions for automatically triggering tests. Currently, when the uploaded test package's "category" or "label" meets the preset conditions, batch tests will be automatically triggered.

```yaml
on:
  bundlePush:
    category:
      - Positioning Optimization
    tag:
      - v0.0.1
```

- **on: Set triggering conditions**

  Used to control when to automatically trigger tests.

- **bundlePush: Set trigger on test package upload**

  When a test package is uploaded and conditions are met, the test will be automatically triggered.

- **category: Test package category**

  Used to specify the category name of the test package that triggers the test.

- **tag: Test package label**

  Used to specify the label name of the test package that triggers the test.

**Notes:**

1. When there is no 'on' or only 'on', batch tests will not be automatically triggered.
2. If there is only 'bundlePush', any uploaded test package will automatically trigger the batch test.
3. With 'category' or 'tag', only test packages that meet preset conditions will trigger the batch test.

<br />

## Output Test Results {#save-artifacts}

In the 'script' field of the configuration file, use the `pytest --junitxml=path` command to create an XML format file at `path` as the result file. Example:

```yaml
jobs:
  - name: 'Positioning Test'
    type: 'generic'
    images:
      base: cr.coscene.cn/coscene-hello/position:v1.0.0
    parameters:
      script:
        - python
        - --junitxml
        - /cos/artifacts/report.xml
```

<br />

## Generate Shadow Mode Artifacts {#generate-shadow-mode}

In the 'script' field of the configuration file, use the command to output the file to `/cos/outputs` as the test output. Example:

```yaml
jobs:
  - name: 'Positioning Test'
    type: 'generic'
    images:
      base: cr.coscene.cn/coscene-hello/position:v1.0.0
    parameters:
      script:
        - bash
        - '-c'
        - cp /cos/files/output.bag /cos/outputs/#output.bag
```

<br />

## Managing Multiple Tests {#manage-multiple-tests}

A single configuration file can manage multiple batch tests. Use --- as a delimiter between different tests. Example:

```yaml
version: '1'
jobs:
  - name: 'Positioning Test'
    type: 'generic'
    images:
      base: cr.coscene.cn/coscene-hello/position:v1.0.0

---
version: '1'
jobs:
  - name: 'Recognition Test'
    type: 'generic'
    images:
      base: cr.coscene.cn/coscene-hello/recognize:v1.0.0
```

<br />

## Message Notifications {#notifications}

Set up the message notification template: Once the batch test is completed, send a message to the DingTalk group. Example:

```yaml
jobs:
  - name: 'Positioning Test'
    type: 'generic'
    images:
      base: cr.coscene.cn/coscene-hello/position:v1.0.0
    notifications:
      - dingTalkBot:
          accessToken: 4d96da******91246c
          titleTemplate: matrix
          contentTemplate: >-
            {{ job.name }} completed

            Test ID: {{ workflow.number }}

            Associated Workflow: {{ workflow.link }}

            Test Package Triggered: {{ job.test_bundle_filename }}

            Start Time: {{ job.start_time | formatByOffset:"+08:00" }}

            End Time: {{ job.end_time | formatByOffset:"+08:00" }}

            Test Cases: Total: {{ job.total_test_cases }}, Passed: {{ job.success_count }}, Failed: {{ job.fail_count }}

            Images: {% if ("base" in job.image_names) %} {{ job.image_names.base }} {% endif %}{% if ("robot" in job.image_names) %} {{ job.image_names.robot }} {% endif %}

            Test Duration: {{ job.duration }}

            CPU Time Consumed by Test: {{ job.total_machine_time }}

            Parameters:
            {% for key,item in job.parameters.script %}{{ key }}:{{ item }}{% endfor %}
```

- **notifications: Set message notification template**

  Used to control when to send message notifications.

- **dingTalkBot: Notify DingTalk group**

  Currently, only supports sending messages to DingTalk groups.

- **accessToken: Set DingTalk group permissions**

  Set the DingTalk group's token to gain permission to send notifications to the DingTalk group.

- **contentTemplate: Message template content**

  Customize the message template content.

- **Available Variables**

  | Variable Name            | Description                                                        | Type (golang)          |
  | ------------------------ | ------------------------------------------------------------------ | ---------------------- |
  | workflow.link            | URL of the batch test                                              | string                 |
  | workflow.number          | Run ID of the batch test                                           | int                    |
  | job.name                 | Name of the test suite run                                         | string                 |
  | job.start_time           | Start time of the test suite (13-digit unix millisecond timestamp) | int64                  |
  | job.end_time             | End time of the test suite (13-digit unix millisecond timestamp)   | int64                  |
  | job.duration             | Duration of the test suite                                         | string                 |
  | job.total_machine_time   | CPU time consumed by the test, unit: core \* seconds               | string                 |
  | job.total_test_cases     | Total number of test cases executed                                | int                    |
  | job.success_count        | Number of test cases passed                                        | int                    |
  | job.fail_count           | Number of test cases failed                                        | int                    |
  | job.image_names          | Image addresses                                                    | map[string]string      |
  | job.parameters           | 'parameters' in the test suite                                     | map[string]interface{} |
  | job.test_bundle_filename | Name of the test package run                                       | string                 |

**Notes:**

1. Reference: [Django-syntax like templating-language](https://github.com/flosch/pongo2)
2. Custom filters can be implemented.

   a. `formatByOffset:"$offset"`

   Adjust the unix millisecond timestamp to the given [utc-offset](https://en.wikipedia.org/wiki/List_of_UTC_offsets) time zone, and then output it as a string in the [RFC3339](https://www.rfc-editor.org/rfc/rfc3339) format. For [zero timezone](https://en.wikipedia.org/wiki/UTC%2B00:00), please enter "+00:00".

   ```
   # UTC: 2023-05-23T04:21:09Z
   input: { "time": "1684815669768" }

   {{ time | formatByOffset:\"+08:00\" }}

   output: 2023-05-23T12:21:09+08:00
   ```

   b. `naturalDuration:"$timeUnit"`

   Supported timeunit: `second`, `millisecond`. It can be left blank, and the default is `second`.

   Time conversion example:

   ```
   input: { "duration" : "600" }

   {{ duration | naturalDuration:"second" }}

   output: 10m0s
   ```
