---
sidebar_position: 4
---

# Postman 使用

## 什么是 Postman？

Postman 是一个用于构建和使用 API 的 API 平台。Postman 简化了 API 生命周期的每个步骤并简化了协作，因此您可以更快地创建更好的 API。
[Postman 软件下载地址](https://www.postman.com/)

## 如何使用 Postman？

### 导入 OpenAPI 定义文件，创建接口集合

![postman-import](./img/postman-import.png)

在地址栏中输入 `https://download.coscene.cn/openapi/openapi.yaml` 刻行对应的 OpenAPI 定义文件地址，导入新的 OpenAPI 接口定义。

### 自定义变量信息

![postman-variable](./img/postman-variable.png)

按照如图所示，用户可以手动修改部分变量信息。

### 调试接口

我们以 GetOrganization 接口为例，使用 Postman 进行接口调用。

#### 填写用户名和密码

![get-org-1](./img/postman-get-org-1.png)

如图所示，在 Postman 中使用 Basic Auth，填写入对应的用户名和密码。用户名固定为 `apikey`，密码为网页端生成的 apikey。

#### 填写请求信息

![get-org-2](./img/postman-get-org-2.png)

在请求变量 `organization` 中写入 `current`，表示获取用户当前的组织信息。然后发送请求。

#### 查看返回信息

![get-org-3](./img/postman-get-org-3.png)

如图所示，接口返回了用户对应的组织信息。
