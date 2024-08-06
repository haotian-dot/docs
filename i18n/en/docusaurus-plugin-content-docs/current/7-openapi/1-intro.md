---
sidebar_position: 1
---

# Introduction

You can use coScene's open platform OpenAPI to build scripts and applications for automated workflows, system integration, and extending application functionalities.

Before making API calls, please follow these steps:

1. [Obtain the OpenAPI endpoint](./2-openapi-endpoint.md). The endpoint of the OpenAPI will vary depending on the version of coScene products you are using. Refer to your current platform address to obtain the latest endpoint.

2. [Retrieve API key through authorization](./3-apikey.md). All open interfaces require authentication using an API key. Please keep it safe and do not upload it to public platforms.

After completing the above steps, you can start using coScene's OpenAPI platform.

## Swagger

coScene provides an OpenAPI YAML file compliant with the OpenAPI 3.0.3 standard, which can be downloaded from [OpenAPI YAML](https://download.coscene.cn/openapi/openapi.yaml). You can also directly access the [Swagger Editor](https://petstore.swagger.io/?url=https://download.coscene.cn/openapi/openapi.yaml) to view information about related interfaces online.

## SDK

coScene OpenAPI provides SDKs for various languages, and you can view information about supported language SDKs on [buf](https://buf.build/coscene-io/coscene-openapi/sdks).

## Examples

For different SDKs, coScene provides example codes in commonly used languages such as Go, Java, and Python, available at the [openapi-example](https://github.com/coscene-io/openapi-example) project. If you need example code in other languages, please contact coScene developers for assistance.
