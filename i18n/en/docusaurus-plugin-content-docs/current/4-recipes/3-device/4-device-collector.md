---
sidebar_position: 4
---

# 数采规则

> 准入的设备可按数据采集规则，将数据自动上传到项目中。数采规则应用于所有设备共用一套配置，如果需要按照项目划分采集规则，请参考[关于数据自动采集与诊断](../9-data-diagnosis/1-intro.md) 使用规则引擎来处理满足相关需求。

## 关于数采规则

> 数采规则应用于组织中的全部设备，仅组织管理员可编辑

数采规则定义需要监控的设备日志所在目录、设备信息文件的存放目录等。当设备准入之后，设备会主动拉取组织配置的数采规则信息，依据配置的规则在机器端动态运行。

## 编辑数采规则

数采规则的结构格式参见下文。

进入组织管理页面的「设备」分页，点击【编辑数采规则】按钮。

![org-device](../img/org-device.png)

在线编辑数采规则，在完成配置后点击【保存编辑】。

![org-dev-rule-save](../img/org-dev-rule-save.png)

## 数采规则格式

数采规则主要对三个模块进行设置：

- **数据收集器设置（collector）**：完成数据采集后，是否删除设备端数据
- **存储设置（mod）**：设备端数据的存储目录；设备标识文件的地址
- **更新设置（updater）**：当前程序是否开启自动更新

示例数采设备信息文件如下：

```yaml
collector:
  delete_after_upload: true # 默认值为 False
  delete_after_interval_in_hours: 48 # 默认值为 -1，即不删除文件
  scan_interval_in_secs: 60 # 默认值：60，即 60s 对文件夹扫描一次

mod:
  name: 'default' # mod 名称，默认 default，定制版请联系刻行产品了解详细信息
  conf:
    enabled: true # 是否启用，默认为 true
    robot_file: '/root/.ros/sn.txt' # 设备标识文件，用于存放设备唯一标识码，如 sn
    # 设备端的监听目录，作为项目中数据采集任务与规则采集的指定目录
    base_dirs:
      - /home/bag/
      - /home/log/

updater:
  enabled: false # Enable Auto Update, default false
```

### 数据收集器设置

设置完成数据采集后，是否删除设备端数据，以释放设备端硬盘存储

```yaml
# 数据收集器设置
collector:
  delete_after_upload: true # 默认值为 False
  delete_after_interval_in_hours: 48 # 默认值为 -1，即不删除文件；否则默认会删除 48 小时以前的旧数据
  scan_interval_in_secs: 60 # 默认值：60，即 60s 对文件夹扫描一次
```

### 存储设置

设置设备端数据的存储地址

```yaml
# 数据处理设置，可定制，具体信息请咨询刻行产品了解详细过程
mod:
  name: 'default' # mod 名称，默认 default，定制版请联系刻行产品了解详细信息
  conf:
    enabled: true # 是否启用，默认为 true
    robot_file: '/root/.ros/sn.txt' # 设备标识文件，用于存放设备唯一标识码，如 sn
    # 设备端的监听目录，作为项目中数据采集任务与规则采集的指定目录
    base_dirs:
      - /home/bag/
      - /home/log/
```

### 更新设置

设置是否自动更新数采程序

```yaml
# 更新设置
updater:
  enabled: true # 是否自动更新数采程序，默认值为 true
```
