# ZYC Assist Pro 自动发布工作流

这个仓库包含了 ZYC Assist Pro 的自动发布工作流配置。当你推送代码到主分支时，GitHub Actions 将自动创建一个新的发布版本，并上传当前目录中的所有文件。

## 工作流程

1. 当代码推送到 `main` 或 `master` 分支时，工作流自动触发
2. 从 `latest.json` 文件中读取当前版本号
3. 自动收集当前目录下的所有文件（排除 .git、.github 目录和 .DS_Store 文件）
4. 创建一个新的 GitHub Release，版本号为 `v{版本号}`
5. 上传所有收集到的文件到该 Release

## 如何使用

1. 确保你的项目中有 `latest.json` 文件，并包含正确的版本信息
2. 将需要发布的文件放在项目根目录下
3. 推送代码到 `main` 或 `master` 分支
4. GitHub Actions 将自动创建一个新的发布版本

## latest.json 文件格式

```json
{
  "version": "0.1.4",
  "notes": "点击下方资源下载此版本",
  "pub_date": "2025-05-17T03:40:06.196Z",
  "platforms": {
    // 平台相关信息
  }
}
```

## 注意事项

- 确保你的仓库有足够的权限来创建 Release
- 大文件可能需要使用 Git LFS
- 如需修改工作流配置，请编辑 `.github/workflows/release.yml` 文件 