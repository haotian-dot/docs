---
sidebar_position: 2
---

# 获取授权和 Token 认证

![apikey](./img/apikey-1-zh.png)

在刻行平台中，按照图示步骤（右上角头像 -> 个人设置 -> 安全 -> 生成访问令牌）生成您的个人 API 密钥 (apikey)。生成的 API 密钥的权限范围与您当前账户一致，请勿将个人 API 密钥上传至公开平台，以避免信息泄露等问题。

## 认证

刻行平台对 OpenAPI 使用 Basic Auth 模式进行认证。认证逻辑为 Base64(username:password)，其中 username 固定为 “apikey”，password 为您生成的 API 密钥。
