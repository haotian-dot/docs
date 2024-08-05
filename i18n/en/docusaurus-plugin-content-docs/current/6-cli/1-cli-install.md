---
sidebar_position: 1
---

# Installation and Initialization

## Installation

Run the following command in the terminal to install the latest version of the Coscene CLI tool:

```Bash
curl -fL https://download.coscene.cn/coscli/install.sh | sh
```

You can use `coscli -h` in the terminal to confirm that the CLI tool has been successfully installed and to see the basic usage of the tool.
![coscli-help](./img/coscli-help.png)

### Update to the Latest Version

```Bash
coscli update
```

## Login

The coScene CLI tool requires your personal access token to work. You can generate an access token on the [coScene - My Settings](https://coscene.cn/profile?section=security) page.

The CLI tool also requires you to specify a default project as the default environment for all operations. Please select the project you want to work on and get the project slug from the URL.

![project-slug-url](./img/project-slug-url.png)

### Configure CLI Permissions

```Bash
# Replace <project slug> after -p
# Replace <personal access token> after -t
coscli login set -p <project slug> -t <personal access token>
```

## Switch Default Project

After successfully authenticating the CLI, you can use the command line to switch the default working project. First, we can list all the projects in the organization that the user has access to, along with their corresponding project slugs:

```
coscli project list
```

![coscli-list-user-projects](./img/coscli-list-user-projects.png)

After finding the target project, use `coscli login set` to update the default working project. If needed, you can use `coscli login current` to confirm.

```bash
coscli login set -p starbase
coscli login current
```

![coscli-update-default-project-slug](./img/coscli-update-default-project-slug.png)
