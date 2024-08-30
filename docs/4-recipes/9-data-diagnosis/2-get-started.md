---
sidebar_position: 2
---

# 实现你的数据采集与诊断

以设定场景为例，实现你的数据自动采集与诊断：

- 当设备 dev-A 的 log 中出现字段「error 1」时，上传 log 文件到记录中，并在字段出现的时间点创建一刻

<br />

## 前提条件

1. 请准备好一台设备

2. 请创建名为 auto-upload 的项目，详情参见[创建项目](https://docs.coscene.cn/docs/get-started/create-project-flow#3-%E5%88%9B%E5%BB%BA%E9%A1%B9%E7%9B%AE)。

3. 请确认你在 coScene 的组织角色为「管理员」。若不是管理员，请联系组织管理员更新你的组织角色。

   ![org-role](../img/org-role.png)

<br />

## 在项目中添加规则

1. 进入 auto-upload 项目

   ![pro-1](../img/pro-1.png)

2. 在项目中，进入「数采&诊断规则」分页，点击【添加规则组】

   ![data-2-1](../img/9-add-rule-set.png)

3. 更改规则组名称后，点击【添加空白规则】

   ![data-2-2](../img/9-add-rule.png)

4. 更改规则名称，复制规则 `"error 1" in log` 到触发条件，勾选触发操作中的生成记录和创建一刻，更改一刻名称为 `触发了 error 1`，点击【创建】

   ![pro-rule-base-rule](../img/pro-rule-base-rule-1.png)

   ![pro-rule-base-rule](../img/pro-rule-base-rule-2.png)

5. 回到「数采&诊断规则」页面，选择刚刚添加的规则组，点击启用按钮

   ![data-2-3](../img/9-enable-rule-set.png)

   \*更多规则条件样式参见[规则的结构与示例](./3-add-rule.md#常用规则条件示例)

<br />

## 在项目中添加数据诊断触发器

1. 进入 auto-upload 项目

   ![pro-1](../img/pro-1.png)

2. 在项目中，进入「自动化-触发器」页面，点击【创建触发器】

   ![pro-trigger-add](../img/pro-trigger-add.png)

3. 编辑触发器内容

- 编辑触发器名称为「数据诊断」，
- 选择关联动作为「系统动作」，
- 从系统动作下拉框中「数据诊断」
- 编辑文件通配符模式为`**/*` (格式使用 Glob，详细可查看[参考文档](https://www.malikbrowne.com/blog/a-beginners-guide-glob-patterns/))
- 点击【创建触发器】

  ![pro-trigger-base](../img/pro-trigger-edit.png)

<br />

## 配置数采设备信息

1. 进入组织管理页面的「设备」分页，点击【编辑数采规则】按钮

   ![org-device-1](../img/org-device-1.png)

2. 清空规则中的默认内容后，复制下述规则，粘贴在编辑器中

   ```yaml
   mod:
     name: 'default' # mod 名称，默认 default，定制版请联系刻行产品了解详细信息
     conf:
       enabled: true # 是否启用，默认为 true
       base_dir: '/root/logs/' # 数据监听目录

   event_code: # 错误码功能
     enabled: false # 错误码白名单配置，默认 False
   ```

   \*更多配置参见[数采规则格式](https://docs.coscene.cn/docs/receipts/device/device-authorize#%E6%95%B0%E9%87%87%E8%A7%84%E5%88%99%E6%A0%BC%E5%BC%8F)

3. 点击【保存编辑】按钮

   ![org-device-7](../img/org-device-7.png)

<br />

## 准入设备

> 以 linux 设备为例。

<br />

1. 打开设备终端，执行以下命令并输入密码，进入 root

   ```
   sudo su
   ```

2. 在设备终端，创建文件监听目录 `/root/logs`

   ```
   mkdir logs
   ```

3. 在刻行平台，进入组织管理页面的「设备」分页， 点击【添加设备】

   ![org-device](../img/org-device-add.png)

4. 在弹窗中选择【从设备端添加】，复制安装命令，以 root 账户粘贴到设备终端

   ![org-device-copy-command](../img/org-device-copy-command.png)

5. 在设备终端执行命令，查看日志

   ```
    journalctl -fu cos
   ```

   - 当日志中出现如下字段时，表示已安装完毕，设备正在等待管理员审核

     ![dev-install-1](../img/dev-install-1.png)

6. 在组织管理页面的「设备」分页，找到需要审核的设备，点击【准入数采】

   ![org-device-authorize](../img/org-device-authorize.png)

<br />

## 将设备添加到项目里

1.  在项目的「项目设备」分页，点击【添加设备】

    ![pro-device-add](../img/pro-device-add-1.png)

2.  勾选需要添加的设备，点击【确定】

    ![pro-device-add-2](../img/pro-device-add-2.png)

## 在设备监听目录中写入文件

1. 确认设备已获取到数采与诊断规则

   - 当日志中出现如下字段时，表示已成功获取到规则

     ![rule-log-1](../img/rule-log-1.png)

2. <a href="https://coscene-artifacts-prod.oss-cn-hangzhou.aliyuncs.com/docs/4-recipes/data-diagnosis/dev-A.log.zip" download>点击此处下载</a> 设备 dev-A 生成的 dev-A.log。其内容如下：

   ```
   2023-09-01 11:28:47.000 INFO "Demo Log message 1"
   2023-09-01 11:28:48.000 INFO "Demo Log message 2"
   2023-09-01 11:28:49.000 INFO "Demo Log message 3"
   2023-09-01 11:28:50.000 WARN "Demo Log message 4"
   2023-09-01 11:28:51.000 INFO "Demo Log message 5"
   2023-09-01 11:28:52.000 INFO "Demo Log message 6"
   2023-09-01 11:28:53.000 INFO "Demo Log message 7"
   2023-09-01 11:28:54.000 INFO "Demo Log message 8"
   2023-09-01 11:28:55.000 INFO "Demo Log message 9"
   2023-09-01 11:28:56.000 INFO "Demo Log message 10"
   2023-09-01 11:28:57.000 WARN "Demo Log message 11"
   2023-09-01 11:28:58.000 ERROR "Demo Log message 12 error 1"
   2023-09-01 11:28:59.000 INFO "Demo Log message 13"
   2023-09-01 11:29:00.000 INFO "Demo Log message 14"
   2023-09-01 11:29:01.000 INFO "Demo Log message 15"
   2023-09-01 11:29:02.000 INFO "Demo Log message 16"
   2023-09-01 11:29:03.000 INFO "Demo Log message 17"
   2023-09-01 11:29:04.000 INFO "Demo Log message 18"
   2023-09-01 11:29:05.000 INFO "Demo Log message 19"
   2023-09-01 11:29:06.000 INFO "Demo Log message 20"
   ```

3. 在本机终端执行命令，将文件 dev-A.log 复制到设备端 `/root/logs/` 中

   ```
   scp Downloads/dev-A.log root@ubuntu:/root/logs

   # 其中 Downloads/dev-A.log 为本机 dev-A.log 文件所在目录，root@ubuntu 为设备名称，二者需按实修改
   ```

4. log 数据上传

   - 当日志中出现如下字段时，表示 log 数据正在上传到刻行时空平台

     ![rule-log-2](../img/rule-log-2.png)

<br />

## 查看创建的记录

1. 进入 auto-upload 项目

   ![pro-1](../img/pro-1.png)

2. 查看自动创建的记录

   ![auto-record-1](../img/auto-record-1.png)

3. 查看记录中上传的数据

   ![auto-record-2](../img/auto-record-2.png)

4. 查看在触发时间点创建的一刻

   ![auto-record-3](../img/auto-record-3.png)

<br />
