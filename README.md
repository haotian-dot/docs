<img src="./logo.png" alt="coScene Logo" width="250"/>

## 准备工作

- [Node.js >= 20](https://nodejs.org/)
- [pnpm](https://pnpm.io/installation)

## 本地开发

1. 克隆本仓库
2. 安装依赖 `pnpm install`
3. 启动本地环境 `pnpm start`

### 尝试本地构建

`pnpm build && pnpm serve`

### 部署

`master` 分支上的代码会被自动编译部署到生产环境。

参看 [GitHub Action 定义](.github/workflows/deploy-to-oss.yml) 查看部署流程的细节

### 联系方式

如果您有任何问题，您可以创建一个 issue 或联系 contact@coscene.io

### 如何贡献

#### 国际化 i18n

1. 在 /docs 文件夹中编写中文（zh）文档
2. 将文档复制到 i18n/en/docusaurus-plugin-content-docs/current 中并进行适当翻译。
3. 其他页面、模板和组件，请参考 docusaurus 的 i18n 指南

#### 注意：

`docusaurus-plugin-content-docs` 插件是按版本划分内容的。`./docs` 文件夹中的数据将在当前子文件夹和 `current.json` 文件中翻译。

### 其他

请见 贡献指南

### 已知错误

在章节/类别转换时导航按钮的翻译有问题，这是一个官方已经在解决的问题了。

[GitHub Issue #8123](https://github.com/facebook/docusaurus/pull/8123)

## Prerequisite

- [Node.js >= 20](https://nodejs.org/)
- [pnpm](https://pnpm.io/installation)

## Development

1. Install dependencies. `pnpm install`
2. Run dev server. `pnpm start`

### Try a local prod build

`pnpm build && pnpm serve`

## Deploy

Push the changes to the `master` branch. And the GitHub action will automatically try to build and deploy
the content to https://docs.coscene.cn

See the [action file](.github/workflows/deploy-to-oss.yml) for details.

## Contact

If you have any questions, fill free to open an issue or reach out to contact@coscene.io

## How to contribute

### i18n

TL;DR Write the original document in the `/docs` folder, copy it to `i18n/en/docusaurus-plugin-content-docs/current` and do the proper translation.

Other pages, templates, and components, please refer to [docusaurus's i18n guide](https://docusaurus.io/docs/i18n/introduction)

#### Note:

The `docusaurus-plugin-content-docs` plugin always divides its content by versions. The data in `./docs` folder will be translated in the current subfolder and `current.json` file.

### Everything else

See [contribute guide](https://docs.coscene.cn/docs/contribute)

### Known Bugs

There's a bug that prevents the translation of the nav button from showing up correctly when transitioning between chapters/categories. The official team is still working on this issue:

[GitHub Issue #8123](https://github.com/facebook/docusaurus/pull/8123)
