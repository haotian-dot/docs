# 在动作中使用命令行工具

刻行的动作中也内置了使用命令行工具的所需参数，用户只需要在动作对应的镜像中包含刻行的命令行
工具，就可以在动作执行的过程中根据需要调用命令行工具。

文本将指引你编写一个刻行动作，在动作调用过程中，使用命令行工具创建刻行记录，并自动完成上传文件和打标签的过程。

本文中用到的所有源代码都在这个仓库中。

## 准备脚本文件

我们准备在这个动作中，做如下操作

1. 生成 5 个文件夹，以 cli-action-folder 1-5 命名;
2. 在这 5 个文件夹内，随机放入 1-10 个完全随机内容的文件;
3. 使用命令行工具，为 5 个文件夹创建 5 个云端记录，并上传所有文件夹内的文件
4. 随后遍历这 5 个记录，统计里面的文件数目 N ，为记录打上 files: N 的标签

我们的脚本文件如下

```bash
#!/bin/bash

# 创建 5 个文件夹，命名为 cli-action-folder1 到 cli-action-folder5
for i in {1..5}; do
    mkdir -p "cli-action-folder${i}"

    # 在每个文件夹内生成 1 到 10 个随机内容的文件
    num_files=$((RANDOM % 10 + 1))  # 生成 1 到 10 的随机数
    for j in $(seq 1 $num_files); do
        # 使用 /dev/urandom 生成随机内容，并将其输出到文件中
        dd if=/dev/urandom of="cli-action-folder${i}/file${j}.txt" bs=1 count=$((RANDOM + 128)) 2>/dev/null
    done
done

echo "文件夹和文件已生成。"

# 开始调用命令行工具


```

## 准备 Dockerf

关于如何认证和使用刻行镜像仓库，请参见[推送镜像](../8-regression/2-image-management.md)
