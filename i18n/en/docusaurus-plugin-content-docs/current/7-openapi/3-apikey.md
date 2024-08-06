---
sidebar_position: 2
---

# Authorization and Token Authentication

![apikey](./img/apikey-1-zh.png)

In the coScene platform, follow the steps shown (Profile Icon -> Personal Settings -> Security -> Generate Access Token) to generate your personal API key (apikey). The permissions of the generated API key match those of your current account. Do not upload your personal API key to public platforms to avoid information leakage and other issues.

## Authentication

The coScene platform uses Basic Auth for OpenAPI authentication. The authentication logic is Base64(username:password), where the username is fixed as “apikey”, and the password is your generated API key.
