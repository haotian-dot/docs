---
sidebar_position: 98
---

# 自动补全

cos 为 Bash、Zsh 提供自动补全功能，可以为你节省大量的输入。

## macOS系统

### Zsh

cos 通过命令 `cos completion zsh` 生成 Zsh 自动补全脚本。 在 Shell 中导入（Sourcing）该自动补全脚本，将启动 cos 自动补全功能。

为了在所有的 Shell 会话中实现此功能，请将下面内容加入到文件 `~/.zshrc` 中。

```Bash
source <(cos completion zsh)
```

重新加载 Shell 后，cos 自动补全功能将立即生效。

如果你收到 `2: command not found: compdef` 这样的错误提示，那请将下面内容添加到 `~/.zshrc` 文件的开头：

```Bash
autoload -Uz compinit
compinit
```

### Bash

cos 的 Bash 补全脚本可以通过 `cos completion bash` 命令生成。 在你的 Shell 中导入（Sourcing）这个脚本即可启用补全功能。

此外，cos 补全脚本依赖于工具 **[bash-completion](https://github.com/scop/bash-completion)**， 所以你必须先安装它。

**警告：**

bash-completion 有两个版本：v1 和 v2。v1 对应 Bash 3.2（也是 macOS 的默认安装版本）， v2 对应 Bash 4.1+。cos 的补全脚本**无法适配** bash-completion v1 和 Bash 3.2。 必须为它配备 **bash-completion v2** 和 **Bash 4.1+**。 有鉴于此，为了在 macOS 上使用 cos 补全功能，你必须要安装和使用 Bash 4.1+。 后续说明假定你用的是 Bash 4.1+（也就是 Bash 4.1 或更新的版本）。

#### 升级 Bash

后续说明假定你已使用 Bash 4.1+。你可以运行以下命令检查 Bash 版本：

```Bash
echo $BASH_VERSION
```

如果版本太旧，可以用 Homebrew 安装/升级：

```Bash
brew install bash
```

重新加载 Shell，并验证所需的版本已经生效：

```Bash
echo $BASH_VERSION $SHELL
```

Homebrew 通常把它安装为 `${brew --prefix}/bin/bash`。

#### 安装 bash-completion

**说明：**

如前所述，本说明假定你使用的 Bash 版本为 4.1+，这意味着你要安装 bash-completion v2 （不同于 Bash 3.2 和 bash-completion v1，cos 的补全功能在该场景下无法工作）。

你可以用命令 `type _init_completion` 测试 bash-completion v2 是否已经安装。 如未安装，用 Homebrew 来安装它：

```Bash
brew install bash-completion@2
```

如命令的输出信息所显示的，将如下内容添加到文件 `~/.bash_profile` 中：

```Bash
brew_etc="$(brew --prefix)/etc" && [[ -r "${brew_etc}/profile.d/bash_completion.sh" ]] && . "${brew_etc}/profile.d/bash_completion.sh"
```

重新加载 Shell，并用命令 `type _init_completion` 验证 bash-completion v2 已经恰当的安装。

#### 启用 cos 自动补全功能

你现在需要确保在所有的 Shell 环境中均已导入（sourced）cos 的补全脚本， 有若干种方法可以实现这一点：

- 在文件 `~/.bash_profile` 中导入（Source）补全脚本：

```Bash
echo 'source <(cos completion bash)' >>~/.bash_profile
```

- 将补全脚本添加到目录 `/usr/local/etc/bash_completion.d` 中：

重新加载 Shell 后，cos 自动补全功能即可生效。 若要在当前 Shell 会话中启用 Bash 补全功能，源引 `~/.bashrc` 文件：

```Bash
source ~/.bashrc
```

## Linux

### Zsh

cos 通过命令 `cos completion zsh` 生成 Zsh 自动补全脚本。 在 Shell 中导入（Sourcing）该自动补全脚本，将启动 cos 自动补全功能。

为了在所有的 Shell 会话中实现此功能，请将下面内容加入到文件 `~/.zshrc` 中。

```Bash
source <(cos completion zsh)
```

重新加载 Shell 后，cos 自动补全功能将立即生效。

如果你收到 `2: command not found: compdef` 这样的错误提示，那请将下面内容添加到 `~/.zshrc` 文件的开头：

```Bash
autoload -Uz compinit
compinit
```

### Bash

cos 的 Bash 补全脚本可以用命令 `cos completion bash` 生成。 在 Shell 中导入（Sourcing）补全脚本，将启用 cos 自动补全功能。

然而，补全脚本依赖于工具 **[bash-completion](https://github.com/scop/bash-completion)**， 所以要先安装它（可以用命令 `type _init_completion` 检查 bash-completion 是否已安装）。

#### 安装 bash-completion

很多包管理工具均支持 bash-completion（参见[这里](https://github.com/scop/bash-completion#installation)）。 可以通过 `apt-get install bash-completion` 或 `yum install bash-completion` 等命令来安装它。

上述命令将创建文件 `/usr/share/bash-completion/bash_completion`，它是 bash-completion 的主脚本。 依据包管理工具的实际情况，你需要在 `~/.bashrc` 文件中手工导入此文件。

要查看结果，请重新加载你的 Shell，并运行命令 `type _init_completion`。 如果命令执行成功，则设置完成，否则将下面内容添加到文件 `~/.bashrc` 中：

```Bash
source /usr/share/bash-completion/bash_completion
```

重新加载 Shell，再输入命令 `type _init_completion` 来验证 bash-completion 的安装状态。

#### 启动 cos 自动补全功能

你现在需要确保一点：cos 补全脚本已经导入（sourced）到 Shell 会话中。 可以通过以下两种方法进行设置：

1. 当前用户

```Bash
echo 'source <(cos completion bash)' >>~/.bashrc
```

1. 系统全局

```Bash
cos completion bash | sudo tee /etc/bash_completion.d/cos > /dev/null
sudo chmod a+r /etc/bash_completion.d/cos
```

**说明：**

bash-completion 负责导入 `/etc/bash_completion.d` 目录中的所有补全脚本。

两种方式的效果相同。重新加载 Shell 后，cos 自动补全功能即可生效。 若要在当前 Shell 会话中启用 Bash 补全功能，源引 `~/.bashrc` 文件：

```Bash
source ~/.bashrc
```
