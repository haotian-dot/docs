---
sidebar_position: 1
---

# Jira

通过集成 Jira，将任务作为故障同步到 Jira 中。

<br />

## 配置集成

> 每个项目单独配置，仅项目管理员可编辑

在项目中，进入「管理项目-服务集成」页面，点击【添加配置】。

![integration-1](../img/integration-1.png)

在线编辑配置，完成配置后点击【保存】。

![integration-2](../img/integration-2.png)

保存成功后，自动启用配置。

![integration-3](../img/integration-3.png)

<br />

## 集成的配置格式

示例配置如下：

```yaml
enabled: true # 启用配置

endpoint: https://jira.com/ # Jira 地址
httpBasicAuthorization:
  usernameAndPassword:
    username: root # Jira 用户名
    password: admin # Jira 密码

projectKey: TEST # Jira 项目 Key

issueTitleTemplate: '{{task.title}}' # Jira 的标题为任务名称
issueDescriptionTemplate: '{{task.title}} {{task.description}} {{record.link}}'# Jira 的描述为任务名称、任务描述、记录链接
issueType: 'Bug' # Jira 类型

customFields: # 自定义字段
  customfield_1:
    id: '88888' # 字段 1（下拉框样式），选择 id 为 88888 的选项
  customfield_2: TEST # 字段 2（文本框样式），输入内容为 TEST
```

- **Jira 项目 Key**

  项目的 Key 需要在 Jira 平台上进行查询，如下：

  ![jira-1](../img/jira-1.png)

- **Jira 类型**

  支持标准字段，如：Bug、Task、Story

- **自定义字段**

  若有自定义字段，请联系刻行。

<br />

## 任务同步到 Jira

> Jira 集成配置完成后，项目中的任务即可同步到 Jira 中。

进入项目的记录页面

![jira-record-1](../img/jira-record-1.png)

在「评论&任务」模块中，点击任务对应的【同步任务】按钮

![jira-record-2](../img/jira-record-2.png)

同步成功后，即展示创建的 Jira 链接。

<br />

## 管理 Jira 集成

### 编辑集成

在项目中，进入「管理项目-服务集成」页面，点击【编辑配置】。

![integration-4](../img/integration-4.png)

在线编辑配置，完成配置后点击【保存】。

![integration-2](../img/integration-2.png)

<br />

### 禁用集成

在项目中，进入「管理项目-服务集成」页面，点击【编辑配置】。

![integration-4](../img/integration-4.png)

将配置中的 `enabled: true` 改为 `enabled: false` 后，点击【保存】。

![integration-2](../img/integration-2.png)

<br />

### 删除集成

在项目中，进入「管理项目-服务集成」页面，点击【编辑配置】。

![integration-4](../img/integration-4.png)

将配置中的内容全部删除后，点击【保存】。

![integration-2](../img/integration-2.png)

<br />
