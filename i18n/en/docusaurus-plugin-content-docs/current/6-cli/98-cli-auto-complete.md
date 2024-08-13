---
slug: auto-complete
sidebar_position: 98
---

# Auto-completion

Cos provides auto-completion functionality for Bash and Zsh, saving you a lot of typing.

## macOS System

### Zsh

Cos generates Zsh auto-completion scripts through the command `cos completion zsh`. Importing (sourcing) this auto-completion script in the shell will enable cos auto-completion.

To enable this feature in all shell sessions, add the following to your `~/.zshrc` file.

```Bash
source <(cos completion zsh)
```

Reload the shell, and the cos auto-completion feature will take effect immediately.

If you receive an error like `2: command not found: compdef`, add the following to the beginning of your `~/.zshrc` file:

```Bash
autoload -Uz compinit
compinit
```

### Bash

The Bash completion script for cos can be generated using the `cos completion bash` command. Sourcing this script in your shell will enable auto-completion.

Additionally, cos completion scripts depend on the tool **[bash-completion](https://github.com/scop/bash-completion)**, so you must install it first.

**Warning:**

There are two versions of bash-completion: v1 and v2. Version 1 corresponds to Bash 3.2 (also the default installed version on macOS), and version 2 corresponds to Bash 4.1+. Cos completion scripts **do not work** with bash-completion v1 and Bash 3.2. It requires **bash-completion v2** and **Bash 4.1+**. Therefore, to use cos completion on macOS, you must install and use Bash 4.1+. The following instructions assume you are using Bash 4.1+.

#### Upgrade Bash

The following instructions assume you are using Bash 4.1+. You can check your Bash version with the following command:

```Bash
echo $BASH_VERSION
```

If the version is too old, you can install/upgrade using Homebrew:

```Bash
brew install bash
```

Reload the shell and verify that the desired version is active:

```Bash
echo $BASH_VERSION $SHELL
```

Homebrew typically installs it as `${brew --prefix}/bin/bash`.

#### Install bash-completion

**Note:**

As mentioned earlier, these instructions assume you are using Bash 4.1+, which means you need to install bash-completion v2 (different from Bash 3.2 and bash-completion v1, where cos completion does not work).

You can test if bash-completion v2 is installed using the command `type _init_completion`. If it is not installed, install it with Homebrew:

```Bash
brew install bash-completion@2
```

As the command output indicates, add the following to your `~/.bash_profile` file:

```Bash
brew_etc="$(brew --prefix)/etc" && [[ -r "${brew_etc}/profile.d/bash_completion.sh" ]] && . "${brew_etc}/profile.d/bash_completion.sh"
```

Reload the shell and verify the installation of bash-completion v2 using the command `type _init_completion`.

#### Enable cos Auto-completion

You now need to ensure that the cos completion script is sourced in all shell environments. There are several ways to achieve this:

- Source the completion script in the `~/.bash_profile` file:

```Bash
echo 'source <(cos completion bash)' >>~/.bash_profile
```

- Add the completion script to the `/usr/local/etc/bash_completion.d` directory:

Reload the shell, and cos auto-completion will take effect. To enable Bash completion in the current shell session, source the `~/.bashrc` file:

```Bash
source ~/.bashrc
```

## Linux

### Zsh

Cos generates Zsh auto-completion scripts through the command `cos completion zsh`. Importing (sourcing) this auto-completion script in the shell will enable cos auto-completion.

To enable this feature in all shell sessions, add the following to your `~/.zshrc` file.

```Bash
source <(cos completion zsh)
```

Reload the shell, and the cos auto-completion feature will take effect immediately.

If you receive an error like `2: command not found: compdef`, add the following to the beginning of your `~/.zshrc` file:

```Bash
autoload -Uz compinit
compinit
```

### Bash

The Bash completion script for cos can be generated using the `cos completion bash` command. Sourcing this script in your shell will enable cos auto-completion.

However, the completion script depends on the tool **[bash-completion](https://github.com/scop/bash-completion)**, so you need to install it first (you can check if bash-completion is installed using the command `type _init_completion`).

#### Install bash-completion

Many package managers support bash-completion (see [here](https://github.com/scop/bash-completion#installation)). You can install it with commands like `apt-get install bash-completion` or `yum install bash-completion`.

These commands will create the file `/usr/share/bash-completion/bash_completion`, which is the main script for bash-completion. Depending on your package manager, you may need to source this file manually in your `~/.bashrc` file.

Reload your shell and run the command `type _init_completion` to check the installation. If it succeeds, you're all set; otherwise, add the following to your `~/.bashrc` file:

```Bash
source /usr/share/bash-completion/bash_completion
```

Reload the shell and run the command `type _init_completion` to verify the installation status of bash-completion.

#### Enable cos Auto-completion

You now need to ensure that the cos completion script is sourced in the shell session. You can set it up in two ways:

1. For the current user:

```Bash
echo 'source <(cos completion bash)' >>~/.bashrc
```

2. System-wide:

```Bash
cos completion bash | sudo tee /etc/bash_completion.d/cos > /dev/null
sudo chmod a+r /etc/bash_completion.d/cos
```

**Note:**

Bash-completion is responsible for sourcing all completion scripts in the `/etc/bash_completion.d` directory.

Both methods will have the same effect. Reload the shell, and cos auto-completion will take effect. To enable Bash completion in the current shell session, source the `~/.bashrc` file:

```Bash
source ~/.bashrc
```
