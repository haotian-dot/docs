## <img src="./logo.jpg" alt="coScene Logo" width="250"/>

Source code of [https://docs.coscene.cn/](https://docs.coscene.cn/). Generated with [docusaurus](https://github.com/facebook/docusaurus).

## Prerequisite

- [Node.js >= 20](https://nodejs.org/)
- [pnpm](https://pnpm.io/installation)

## Development

1. Install dependencies. `pnpm install`
2. Run dev server. `pnpm start`

### Try a local prod build

```bash
pnpm build && pnpm serve
```

## Deploy

Push the changes to the `master` branch.

See the (action file)[.github/workflows/deploy-to-oss.yml] for details.

## Contact

If you have anything, you can open an issue or reach out to contact@coscene.io

## How to contribute

### i18n

TL;DR Write the original document in the `/docs` folder, copy it to `i18n/en/docusaurus-plugin-content-docs/current` and do the proper translation.

Other pages, templates, and components, please refer to [docusaurus's i18n guide] https://docusaurus.io/docs/i18n/introduction

#### Note:

The docusaurus-plugin-content-docs plugin always divides its content by versions. The data in ./docs folder will be translated in the current subfolder and current.json file.

### Everything else

See [contribute guide](https://docs.coscene.cn/docs/contribute)

### Known Bugs

There's a bug that prevents the translation of the nav button from showing up correctly when transitioning between chapters/categories. The official team is still working on this issue:

[GitHub Issue #8123](https://github.com/facebook/docusaurus/pull/8123)
