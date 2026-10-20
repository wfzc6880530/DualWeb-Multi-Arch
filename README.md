# DualWeb Multi-Arch

实验项目：为 DualWeb 提供可选监听端口的独立部署包，并按 ImmortalWrt/OpenWrt 版本分支维护。

## 版本分支约定

- `v24.10`：ImmortalWrt 24.10 系列
- `v25.12`：ImmortalWrt 25.12 系列

每个版本分支都由 GitHub Actions 分别测试 `x86_64` 与 `aarch64`。不要把两个版本的系统包混装。

## 重要的包格式区别

24.10 系列通常使用 opkg / IPK；25.12 系列切换到 apk 包管理，必须用匹配的 25.12 SDK/构建系统制作 APK。不能把 IPK 改名为 APK。本仓库的 CI 首先执行源码交叉编译、静态检查与打包输入检查；只有经过对应版本 SDK 构建及设备安装验证后，才应将产物标记为可安装发行包。

## 当前构建约定

- `x86_64` → Go `GOARCH=amd64`
- `aarch64` → Go `GOARCH=arm64`
- 默认监听端口：8081
- 修改端口：`dualweb-port 8888`
- 不主动修改 LuCI/uhttpd 的 80 端口。
- 不要将 OpenClash/Mihomo API 或管理面板直接暴露到公网。

## 运行 CI

打开 Actions → **DualWeb version/architecture CI**，可在版本分支运行 workflow。每次 push 到 `v24.10` 或 `v25.12` 都会分别执行两个架构的编译和检查。

## 上游源码

默认使用 `https://github.com/wfzc6880530/dualweb` 的 `test/openbox-artifacts` 分支。可通过仓库 Actions Variables 配置 `DUALWEB_REPO_URL` 与 `DUALWEB_REF`。

## 状态

实验中。CI 通过不代表已经在实体设备上验证 Nginx 配置、依赖解析、服务启动、页面/API 路由或卸载行为。请先在备份过的测试设备上验证。
