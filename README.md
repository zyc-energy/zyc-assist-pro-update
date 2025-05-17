# ZYC Assist Pro 自动发布工作流

这个仓库包含了 ZYC Assist Pro 的自动发布工作流配置。当你推送代码到主分支时，GitHub Actions 将自动创建一个新的发布版本，并上传当前目录中的所有文件。

## 工作流程

1. 当代码推送到 `main` 或 `master` 分支时，工作流自动触发
2. 从 `latest.json` 文件中读取当前版本号
3. **自动更新 `latest.json` 文件中的所有 GitHub 仓库 URL 地址为当前仓库地址**
4. 自动收集当前目录下的所有文件（排除 .git、.github 目录和 .DS_Store 文件）
5. 创建一个新的 GitHub Release，版本号为 `v{版本号}`
6. 上传所有收集到的文件到该 Release

## 如何使用

1. 确保你的项目中有 `latest.json` 文件，并包含正确的版本信息
2. 将需要发布的文件放在项目根目录下
3. 推送代码到 `main` 或 `master` 分支
4. GitHub Actions 将自动创建一个新的发布版本，并更新 `latest.json` 中的所有 URL 地址

## latest.json 文件格式

```json
{
  "version": "0.1.6",
  "notes": "查看资产以下载此版本并安装。",
  "pub_date": "2025-05-17T08:23:27.888Z",
  "platforms": {
    "darwin-x86_64": {
      "signature": "...",
      "url": "https://github.com/Hyan08/tauri-test/releases/download/v0.1.6/ZYC.Assist.Pro_x64.app.tar.gz"
    },
    // 其他平台信息
  }
}
```

## URL 自动更新

工作流会自动将 `latest.json` 文件中的所有 GitHub 仓库 URL 更新为当前仓库地址。

例如，以下 URL 都会被正确更新：
- `https://github.com/zyc-energy/zyc-assist-pro/...` 
- `https://github.com/Hyan08/tauri-test/...` 
- 任何其他格式的 GitHub 仓库 URL

更新后的 URL 将指向当前仓库，确保下载链接始终指向正确的发布位置。

## 注意事项

- 确保你的仓库有足够的权限来创建 Release
- 大文件可能需要使用 Git LFS
- 如需修改工作流配置，请编辑 `.github/workflows/release.yml` 文件 