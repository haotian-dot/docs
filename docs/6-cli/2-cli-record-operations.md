---
slug: record-operations
sidebar_position: 2
---

# 使用命令行操作记录（Records）

关于刻行命令行中操作记录的详细信息，您可以使用 `cocli record -h` 来查看详细用法

![cli-record-help](./img/cocli-record-help.png)

以下是一些常见操作的示例：

## 创建记录

```bash
# 创建一个叫做<预留文件>的记录
cocli record create -t 预留文件
```

![cocli-record-create](./img/cocli-record-create.png)

您可以点击结果中的网址，在网页中查看刚创建的记录

## 查看项目中的记录

```bash
cocli record list
```

![cocli-record-list](./img/cocli-record-list.png)

List 命令会将项目中的所有记录列出，我们可以通过串联`grep` 和 `cut` 等命令来获取某个记录的 ID

```bash
cocli record list | grep '预留' | cut -d ' ' -f1
```

![cocli-record-get-id](./img/cocli-record-get-id.png)

## 上传文件到记录

您可以将任意指定的文件或者目录内的文件上传到特定记录，我们以前述的`预留文件`记录为例

```bash
# 创建一个临时文件
touch TEST_FILE

# 将该文件上传到前面创建的 Record
cocli record upload acd706d9-0879-4d88-8550-e69bb8ff8f6b ./TEST_FILE
```

![cocli-upload-file-to-record](./img/cocli-upload-file-to-record.png)

此时再刷新网页中的记录，就可以看到我们刚上传的文件了

![view-just-uploaded-file](./img/view-just-uploaded-file.png)

## 下载记录中的文件

我们也可以将记录中的文件下载到本地，在`预留文件`这个记录中，我们又上传了一些随机文件作为示例。

![cocli-record-download-prepare-files](./img/cocli-record-download-prepare-files.png)

```bash
cocli record download acd706d9-0879-4d88-8550-e69bb8ff8f6b .
```

![cocli-record-download-to-local](./img/cocli-record-download-to-local.png)

命令行工具会将记录中的所有文件打包在以记录 ID 为名字的文件夹内，这个功能在您之后可能会遇到的下载多个记录中帮助您保持文件的独立性，方便管理。

## 删除记录

命令行工具也可以用来删除记录，删除记录是一个非常危险的操作，请在删除时手工确认是否真的需要
删除记录，或者使用 `-f` 标记来强制删除。

![delete-a-record](./img/delete-a-record.png)

## 管理记录的标签

`cocli record list` 可以很方便的看到记录的标签，我们也可以对记录的标签进行更多的操作。我们以列表中的第一个记录举例。

![cocli-labels-list-record](./img/cocli-labels-list-record.png)

### 给记录添加标签

```
cocli record update d253523f-5a8a-40dd-8bd9-2d289367d6ff -l afternoon,rainy
```

记录成功的添加了 afternoon 和 rainy 的标签

![cocli-record-append-labels](./img/cocli-record-append-labels.png)

### 替换记录的已有标签

```
cocli record update d253523f-5a8a-40dd-8bd9-2d289367d6ff --update-labels sunny,morning
```

可以看到现在的记录的标签已经从 afternoon, rainy 更新成了 sunny, morning

![cocli-record-update-labels](./img/cocli-record-update-labels.png)

### 删除指定标签

```
cocli record update d253523f-5a8a-40dd-8bd9-2d289367d6ff --delete-labels sunny
```

通过命令行删除 `sunny` 标签，可以看到现在只剩下了 `morning` 的标签了

![cocli-record-delete-labels-list](./img/cocli-record-delete-labels-list.png)

## 更新记录的原信息

命令行也支持更改记录的名字和描述信息，下列的命令找出了记录中带有 `empty-record` 标签的第一个记录，更新了该记录的
名字和描述，让用户更方便的理解这个记录的意思

```bash
RECORD_ID=$(cocli record list | grep 'empty-record' | head -n1 | cut -d ' ' -f1)
cocli record update $RECORD_ID -t "Fancy Empty Record Title" -d "Do you really need a description for an empty record"
```

![update-record-title-and-description](./img/update-record-title-and-description.png)
