---
sidebar_position: 1
---

# 简介

您可以利用 coScene 的开放平台 OpenAPI 来构建自动化流程的脚本和应用程序，进行系统集成，并扩展应用功能。

在调用接口之前，请确认以下步骤：

1. [获取开放平台实例地址（Endpoint）](./2-openapi-endpoint.md)。开放平台的实例地址会根据用户使用的刻行产品版本而变化，请参考您当前使用的平台地址以获取最新的实例地址。

2. [通过获取授权获取 API 密钥（apikey）](./3-apikey.md)。所有开放接口均需使用 API 密钥进行鉴权，请妥善保管，切勿上传至公开平台。

完成上述步骤后，即可开始使用刻行平台的 OpenAPI。

## Swagger

coScene 提供了符合 OpenAPI 3.0.3 标准的 OpenAPI YAML 文件，可以通过 [OpenAPI YAML](https://download.coscene.cn/openapi/openapi.yaml) 下载。也可以直接访问 [Swagger Editor](https://petstore.swagger.io/?url=https://download.coscene.cn/openapi/openapi.yaml) 在线查看相关的接口的信息。

## SDK

 平台的 OpenAPI 提供了各类语言的 SDK，您可以在 [buf](https://buf.build/coscene-io/coscene-openapi/sdks) 上查看个目前支持的语言 SDK 信息。

## 示例

针对不同 SDK，coScene 提供了常用语言如 Go、Java、Python 的示例代码，可以参考 [openapi-example](https://github.com/coscene-io/openapi-example) 项目。若需要其他语言的代码样例，请联系平台开发人员获取。
