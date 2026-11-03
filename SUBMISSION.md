# dsh.so 插件市场提交资料

> 提交前必须先做一件事：把 GitHub 仓库名从 `-` 改成 `dsh-drive-manager`。
> dsh.so 要求插件 id 匹配 `^[a-z0-9]+(-[a-z0-9]+)*$`，`-` 不符合，会被检查器拒绝。

## 基本信息

| 字段 | 内容 |
|---|---|
| 插件名 | 磁盘分工管家 |
| 包名 / id | `dsh-drive-manager` |
| 版本 | `0.2.0` |
| 仓库 | https://github.com/JKL-3484/dsh-drive-manager |
| 许可证 | MIT |
| 平台 | Windows 10 / 11 |
| DSH 兼容 | `>= 0.2.1-rc.2`（本机实测 `0.2.1-rc.3`） |
| 安装 | `dsh plugin --profile desktop add github:JKL-3484/dsh-drive-manager` |
| 类型 | dsh 插件（可通过 `dsh plugin add` 安装） |

## 一句话简介

自动识别 C/D/E/F… 所有固定盘，用绿/黄/红标出可清理、需确认、系统占用的空间，核对下载目录，并给出多盘分工与迁移建议；只读，不删文件。

## 详细描述

磁盘分工管家是一个面向新手的 Windows 多盘管理面板。它自动识别所有固定盘，不需要配置盘符；每块盘都有独立的容量卡和绿/黄/红计数，点击盘卡片即可只看这一块盘。

- **绿色**：缓存、临时文件等可直接清理的空间，并给出“怎么彻底删”的系统/软件自带方法，避免只删一半。
- **黄色**：个人数据、已安装软件、聊天记录、项目文件、自定义目录；提示先备份、迁移或卸载重装。
- **红色**：Windows、Program Files、ProgramData、还原点、商店应用、虚拟内存等系统占用；说明为什么不能手动删。

还会核对系统下载文件夹、Edge/Chrome、微信、QQ、Steam、百度网盘、联想商店等下载目录，告诉你哪些还在系统盘；并按“系统盘 + 实际数据盘”生成迁移建议。

**只读**：没有删除按钮，不执行删除命令；只有“在资源管理器中打开”。

## 标签 / 分类

- 分类：系统工具 / 磁盘管理
- 标签：`dsh-plugin`、`disk`、`storage`、`cleanup`、`windows`、`multi-drive`

## 截图

- `docs/screenshots/overview.png`
- `docs/screenshots/filter-c.png`
- `docs/screenshots/filter-d.png`
- `docs/screenshots/downloads.png`
- `docs/screenshots/plan.png`
- `docs/screenshots/multi-drive.png`

## 提交前检查

- [ ] 仓库已改名为 `dsh-drive-manager`（Settings → Rename）
- [ ] 给仓库添加 GitHub topic：`dsh-plugin`
- [ ] `package.json` 的 `repository` / `homepage` / `bugs` 已指向新仓库
- [ ] README 安装命令已改为 `github:JKL-3484/dsh-drive-manager`
- [ ] 最新代码已 push 到 `main`
- [ ] 打开 https://www.dsh.so/zh/submit/，粘贴仓库地址
- [ ] 检查器通过后点击“提交到 dsh.so”
- [ ] 在 dsh.so 的提交 Issue 中补充：Windows-only、只读、无网络请求

## 审核说明

- 源码扫描：`plugin/index.js`、`plugin/client.js`，无硬编码密钥、无外联、无删除 API。
- 子进程：仅 `Get-CimInstance`、`reg query`、`explorer.exe`，详见 `SECURITY.md`。
- 权限：只读扫描；大目录按时间预算统计，显示 `≥` 表示部分统计。
