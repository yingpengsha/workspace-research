# Notes

## Initialize

### pnpm-workspace.yaml

pnpm 不像其他几个包管理工具在 package.json 中配置 workspaces 字段，而是需要在根项目的下面新建一个叫做 `pnpm-workspace.yaml` 的文件来专门声明。

```yaml
packages
  - 'packages/*'
```

## Add Dependencies

### To the root project

和 yarn1 的添加依赖如出一辙，都需要添加 `-w` 参数以强调是在根项目添加依赖

```bash
yarn add express -w
yarn add @test/bundler -w # pnpm 也实现了一个叫做 workspace 的协议，所以最终版本号会显示为 `workspace:version`
```

### To the workspace

```bash
yarn workspace @test/cli add @test/bundler express
cd ./packages/cli && yarn add @test/bundler express
```

## Refer

- [Workspace | pnpm](https://pnpm.io/zh/workspaces)