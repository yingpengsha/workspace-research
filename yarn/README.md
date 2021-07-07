# Notes

> ⚠️ 请检查你的 yarn 版本，如果是 yarn2 的版本，你可以在控制台执行这条指令来切换版本： `yarn set version 1`
> ⚠️ yarn1 的 bug 真多，吐血。官方已经不怎么维护了，建议换 yarn2 :)

## nohoist in workspaces

`nohoist` 是指子项目的依赖**不**将依赖交由根项目来统一管理，yarn1 默认是 `nohoist`，主要是方便一些传统项目迁移至 `workspaces`。

但本文演示的内容为 `hoist` 模式，所以在 `workspaces` 配置到 `workspaces.packages`，具体相关内容请参考[官方博客](https://classic.yarnpkg.com/blog/2018/02/15/nohoist/)。

## Initialize

### package.json

在 package.json 配置 `workspaces` 字段

```text
{
  ...
  "workspaces": {
    "packages": [
      "packages/*"
    ]
  },
  ...
}
```

### yarn install

```bash
yarn install # 将会在根项目的 `node_modules` 下生成所有子项目的软链接依赖。
```

## Add Dependencies

### To the root project

```bash
yarn add express -W # 在根项目中执行，必须添加 `-W` 参数以强调确实是未根项目添加依赖，否则 yarn 会抛出错误以提醒开发者
yarn add @test/bundler@1.0.0 # 给根项目添加本地依赖，第一次安装的时候需要加上版本号否则会出错
yarn add @test/bundler@file:packages/bundler # 或者在 yarn1 中安装子项目为依赖需要显式的使用 file 协议
```

### To the workspace

⚠️ yarn1 不支持批量给子项目添加依赖

在 `hoist` 模式下，下面两种添加依赖的方式是一致的，都会将依赖统一收集到顶层管理。

```bash
yarn workspace @test/bundler add express @test/bundler@1.0.0 # 第一次添加本地依赖需要加上版本号
cd ./packages/package-name && yarn add express @test/bundler@1.0.0
```

## Refer

- [Workspaces | Yarn](https://classic.yarnpkg.com/en/docs/workspaces/)
- [Workspaces in Yarn](https://classic.yarnpkg.com/blog/2017/08/02/introducing-workspaces/)
- [nohoist in Workspaces | Yarn Blog](https://classic.yarnpkg.com/blog/2018/02/15/nohoist/)
- [Cannot `yarn add` in workspace package if depending on a local package](https://github.com/yarnpkg/yarn/issues/3973)
