# Notes

> ⚠️ 笔者已经为本项目安装了 yarn2 和 workspaces-tools，请注意。
> ⚠️ 请先通读 yarn2 的[文档](https://yarnpkg.com/getting-started)，基本使用方式，因为 yarn2 改动很大，并且有些 feature 太激进了，所以还是建议使用 pnpm :)

## Initialize

### package.json

在 package.json 配置 `workspaces` 字段，yarn2 workspaces 默认为 `hoist` 模式，所以不需要专门配置 `workspaces.packages`。

```text
{
  ...
  "workspaces": [
    "packages/*"
  ],
  ...
}
```

### yarn workspaces list

可以通过 `yarn workspaces list` 指令查看 workspaces 有哪些

```bash
$ yarn workspaces list
➤ YN0000: .
➤ YN0000: packages/bundler
➤ YN0000: packages/cli    
➤ YN0000: packages/plugin 
➤ YN0000: Done in 0s 4ms 
```

## Add Dependencies

### To the root project

```bash
yarn add express
yarn add @test/bundler # yarn2 实现了一个叫做 workspace 的新协议，所以最终版本号会显示为 `workspace:packages/bundler`
```

### To the workspace

yarn2 依旧不支持直接用指令来批量给所有子项目添加依赖，但可以使用 `yarn workspaces foreach` hack 一下。

在 `hoist` 模式下，下面两种添加依赖的方式是等价的，都会将依赖统一收集到顶层管理。

```bash
yarn workspace @test/cli add @test/bundler express
cd ./packages/cli && yarn add @test/bundler express
```

## Refer

- [Workspaces | Yarn - Package Manager](https://yarnpkg.com/features/workspaces)
