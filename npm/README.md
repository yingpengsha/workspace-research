# Notes

> ⚠️ `npm workspaces` 仍在不停的改动中，请注意你的 npm 版本，即便你是 v7.x 版本的 npm，也可能因为子版本过小而导致部分功能无法完成。

## Initialize

### package.json

在 package.json 配置 `workspaces` 字段

```text
{
  ...
  "workspaces": [
    "packages/*"
  ],
  ...
}
```

### npm install

```bash
npm install # 将会在根项目的 `node_modules` 下生成所有 workspace 的软链接依赖。
```

## Add Dependencies

### To the root project

```bash
npm install express # 在根项目中执行
npm install @test/bundler # 添加子项目为依赖，最终在 package.json 中呈现的版本号为 'file:path/to/sub-workspaces'
```

### To the workspace

```bash
npm install express -ws # 给所有子项目添加依赖
npm install express -w @test/bundler # 指定某个项目添加依赖
cd ./packages/bundler && npm install express # 进去子项目内单独添加，会单独生成依赖文件，不会在顶层统一管理
```

### One workspace depends on another

在子项目里安装的话，会直接下载远程的发布的版本。

```bash
npm install @test/bundler -w @test/cli
```

## Refer

- [npm workspaces](https://docs.npmjs.com/cli/v7/using-npm/workspaces)
