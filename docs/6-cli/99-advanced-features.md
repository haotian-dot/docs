---
slug: advanced-features
sidebar_position: 99
---

# 高级功能

## 切换登录凭证

刻行的命令行工具内置了登录凭证管理系统，高级用户和测试人员可以在不同的组织、项目、和环境中切换登陆凭证，方便测试和管理。

在您有了默认的登陆凭证之后，想要再添加一个登陆凭证时，您可以使用如下命令来添加一个新的登陆凭证

```bash
cocli login add -n <凭证名字> -p <项目Slug> -t <访问令牌>
```

下面的截图展示了添加了一个名为 typ 的登陆凭证

![cocli-add-login-profile](./img/cocli-add-login-profile.png)

我们可以使用如下命令来获取当前所有可用的凭证

```bash
cocli login list
```

![cocli-list-login-profiles](./img/cocli-list-login-profiles.png)

在不同的登陆凭证中间切换也非常容易

```bash
cocli login switch
```

![cocli-login-switch-interactive](./img/cocli-login-switch-interactive.png)

在运行命令后的交互提示中，用箭头来选择想要切换到的登陆凭证，回车确认选择

![cocli-login-switch-confirm](./img/cocli-login-switch-confirm.png)

切换完成之后会提示当前激活的登陆凭证，也可以用如下命令来确认

```
cocli login current
```

## 链接本地文件夹和云端记录

命令行对于云端记录和本地文件夹还提供了`链接`模式，链接之后的记录，上传和下载文件都无需再次指定记录 ID
