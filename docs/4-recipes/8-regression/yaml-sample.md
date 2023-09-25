---
sidebar_position: 8
---

# 配置文件格式与样例

> 你可以通过本章节的内容了解批量测试配置文件的书写规则；同时本章节会提供样例文件以供参考。

<br />

支持解析的配置文件为 yaml 或 yml 类型文件，且名称必须为 **cos.yaml** 或 **cos.yml**。你可以直接复制，或 <a href="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/regression/cos.yaml.zip" download>点击此处下载</a> 示例配置文件并进行修改。其基本结构如下：

## 自定义测试套件 {#customize-testing-bundle}

设置测试套件名称、测试类型，以及用于运行测试的命令

```yaml
version: '1'
jobs:
  - name: '测试定位问题-1'
    type: 'generic'
    images:
      base: cr.coscene.cn/coscene-hello/position:v1.0.0
    parameters:
      script:
        - /bin/sh
        - -c
        - 'echo hello'
```

- **name：测试套件名称**

  自定义测试套件在网页端所展示的名称

- **type：测试类型**

  目前支持的测试类型为：「generic」、「gazebo」

- **images - base：镜像地址**

  镜像是运行批量测试的虚拟环境；你需要在配置文件中指定每个测试套件运行时使用的镜像版本地址

- **parameters - scripts：运行参数**

  用于指定每个测试套件运行的命令

<br />

## 定义多个测试套件(#define-multiple-jobs)

一个批量测试由一个或多个测试套件组成，这些测试套件可以并行测试

```yaml
version: '1'
jobs:
  - name: '测试定位问题-1'

  - name: '测试定位问题-2'
```

<br />

## 利用标签调用记录(#query-records-by-labels)

设置关联记录所用的标签：每个测试用例会使用其关联记录作为测试数据，关联记录为标签符合 labels 条件的记录

```yaml
records:
  labels:
    - '定位问题'
```

- **records - labels：记录对应标签**

  labels 部分书写规则如下：

  - 逻辑运算

    - 支持且仅支持 `AND` `OR` `NOT` 三种逻辑运算符；所有运算符都需要大写
    - 可以使用括号`(` `)`来明确运算符优先级，注意 `OR` 具有更高的优先级，即 `a AND b OR c` 等价于 `a AND (b OR c)`。

    - `NOT` 后只能为标签，不能为表达式，而 `AND` 与 `OR` 后可以为标签或表达式

      例如，`NOT a` 是有效的，而 `NOT (a AND b)` 是无效的（可以将其重写为 `NOT a OR NOT b`）

    - 多行标签之间的关系相当于 `OR`

  - 空格

    - `AND` 和 `OR` 必须在前后各有一个空格； `NOT` 必须在后面有一个空格
    - 标签中不能带有空格

  - 其他

    - 标签中不能包含 `AND` `OR` `NOT`的子字符串，例如 `label_NO` 是一个无效标签

    - 标签中不能包含括号`（` `）`，例如 `(label` 是一个无效标签

    - 纯数字标签必须使用引号 `‘` `’` 括起

<br />

## 指定资源大小(#specify-resources)

批量测试默认提供的资源大小为 1 核 2 G，可以在参数列表中手动指定大小。

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

## 自动触发测试(#auto-triggering)

设置自动触发测试的条件，目前支持：上传的测试包「种类」或「标签」符合预设条件时，自动触发批量测试

```yaml
on:
  bundlePush:
    category:
      - 定位优化
    tag:
      - v0.0.1
```

- **on：设置触发条件**

  用于控制何时自动触发测试

- **bundlePush：设置上传测试包触发**

  当上传测试包时，满足条件则会自动触发测试

- **category：测试包种类**

  用于指定触发测试的测试包种类名称

- **tag：测试包标签**

  用于指定触发测试的测试包标签名称

**备注：**

1. 没有 on 或者只有 on 时，不会自动触发批量测试
2. 有且仅有 bundlePush 时，任意的测试包上传都会自动触发批量测试
3. 有 category 或者 tag 时， 只有符合预设条件的测试包会自动触发批量测试

<br />

## 输出测试结果文件(#save-artifacts)

在配置文件的 「script 」字段中，使用 `pytest --junitxml=path` 命令在 `path` 处创建一个 XML 格式的文件作为结果文件，示例如下：

```yaml
jobs:
  - name: '测试定位问题'
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

## 输出影子模式文件(#generate-shadow-mode)

在配置文件的 「script」字段中，使用命令将文件输出至 `/cos/outputs` 目录下作为测试输出，示例如下：

```yaml
jobs:
  - name: '测试定位问题'
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

## 管理多个测试(#manage-multiple-tests)

同一配置文件中可管理多个批量测试，使用`---`作为不同测试之间的分隔符，示例如下：

```yaml
version: '1'
jobs:
  - name: '测试定位问题'
    type: 'generic'
    images:
      base: cr.coscene.cn/coscene-hello/position:v1.0.0

---
version: '1'
jobs:
  - name: '测试识别问题'
    type: 'generic'
    images:
      base: cr.coscene.cn/coscene-hello/recognize:v1.0.0
```

<br />

## 消息通知(#notifications)

设置发送消息通知的模板：当批量测试运行完成后，发送消息到钉钉群，示例如下：

```yaml
jobs:
  - name: '测试定位问题'
    type: 'generic'
    images:
      base: cr.coscene.cn/coscene-hello/position:v1.0.0
    notifications:
      - dingTalkBot:
          accessToken: 4d96da******91246c
          titleTemplate: matrix
          contentTemplate: >-
            {{ job.name }}运行完成

            测试编号: {{ workflow.number }}

            所属工作流: {{ workflow.link }}

            触发测试代码包: {{ job.test_bundle_filename }}

            开始时间: {{ job.start_time | formatByOffset:"+08:00" }}

            结束时间: {{ job.end_time | formatByOffset:"+08:00" }}

            测试用例: 总数: {{ job.total_test_cases }}，成功: {{ job.success_count }}, 失败: {{ job.fail_count }}

            镜像: {% if ("base" in job.image_names) %} {{ job.image_names.base }} {% endif %}{% if ("robot" in job.image_names) %} {{ job.image_names.robot }} {% endif %}

            测试时长: {{ job.duration }}

            测试所消耗核时: {{ job.total_machine_time }}

            参数:
            {% for key,item in job.parameters.script %}{{ key }}:{{ item }}{% endfor %}
```

- **notifications：设置消息通知模板**

  用于控制何时发送消息通知

- **dingTalkBot：通知到钉钉群**

  目前仅支持发送消息到钉钉群

- **accessToken：设置钉钉群权限**

  设置钉钉群的 token，以便有发送通知到钉钉群的权限

- **contentTemplate：消息模版内容**

  自定义消息模板内容

- **可用变量**

  | 变量名称                 | 说明                                                    | 类型（golang）         |
  | ------------------------ | ------------------------------------------------------- | ---------------------- |
  | workflow.link            | 批量测试的 URL 地址                                     | string                 |
  | workflow.number          | 批量测试的运行编号                                      | int                    |
  | job.name                 | 运行的测试套件名称                                      | string                 |
  | job.start_time           | 测试套件的测试开始时间（13 位 unix millisecond 时间戳） | int64                  |
  | job.end_time             | 测试套件的测试结束时间（13 位 unix millisecond 时间戳） | int64                  |
  | job.duration             | 测试套件的测试持续时间                                  | string                 |
  | job.total_machine_time   | 测试消耗的 CPU 时间，单位：核 \* 秒                     | string                 |
  | job.total_test_cases     | 测试执行的用例总数                                      | int                    |
  | job.success_count        | 通过的测试用例数量                                      | int                    |
  | job.fail_count           | 失败的测试用例数量                                      | int                    |
  | job.image_names          | 镜像地址                                                | map[string]string      |
  | job.parameters           | 该测试套件中的 「parameters」                           | map[string]interface{} |
  | job.test_bundle_filename | 运行的测试包名称                                        | string                 |

**备注：**

1. 参考资料：[Django-syntax like templating-language](https://github.com/flosch/pongo2)
2. 刻行自定义 filter

   a. `formatByOffset:"$offset"`

   将 unix millisecond 时间戳调整到给定 [utc-offset](https://en.wikipedia.org/wiki/List_of_UTC_offsets) 所在时区后以 [RFC3339](https://www.rfc-editor.org/rfc/rfc3339) 的格式输出字符串。[零时区](https://en.wikipedia.org/wiki/UTC%2B00:00)请填写“+00:00”。

   ```
   # UTC: 2023-05-23T04:21:09Z
   input: { "time": "1684815669768" }

   {{ time | formatByOffset:\"+08:00\" }}

   output: 2023-05-23T12:21:09+08:00
   ```

   b. `naturalDuration:"$timeUnit"`

   支持的 timeunit：`second`, `millisecond`。可以不填，默认为 `second`。

   时间转化示例：

   ```
   input: { "duration" : "600" }

   {{ duration | naturalDuration:"second" }}

   output: 10m0s
   ```
