# 插件市场提交资料

> 这里有两个不同的市场，别混：
>
> - **dsh-market**（你发的 <https://github.com/dsh-market/dsh-market>）：DSH 内的可视化插件市场，目录来自 `awesome-dsh-plugin` 仓库；收录方式是**向 `awesome-dsh-plugin` 提 PR，加一个 YAML**。
> - **dsh.so**（<https://www.dsh.so/zh/submit/>）：另一个社区插件索引；收录方式是在网页提交仓库地址、跑检查、点提交。
>
> 两个可以都做，但**不是同一个入口**。

## 一、dsh-market 收录（推荐先做）

### 提交方式

1. Fork：<https://github.com/awesome-dsh-plugin/awesome-dsh-plugin>
2. 在你的 fork 里新建一个文件：

```text
data/plugins/JKL-3484__dsh-drive-manager.yml
```

3. 内容：

```yaml
url: https://github.com/JKL-3484/dsh-drive-manager
name: JKL-3484/dsh-drive-manager
category: tools
description:
  en: "Windows multi-drive dashboard that labels cleanable, caution, and system space in green, yellow, and red, audits download folders, and suggests how to split data across drives."
  zh: "Windows 多盘磁盘分工面板：用绿/黄/红标出可清理、需确认、系统占用，核对下载目录，并给出多盘分工与迁移建议。"
```

4. 对这个 fork 开 PR，目标 `awesome-dsh-plugin/awesome-dsh-plugin:main`。
5. PR 标题：`Add JKL-3484/dsh-drive-manager`
6. 等 CI + 维护者审核；README 会自动生成，不需要手动改。

### 已满足的收录条件

- `package.json` 声明了 `dsh.bundle.patch`（`./cordis.patch.yml`）✅
- 仓库根有 `cordis.patch.yml` ✅
- 有真实可用代码（`plugin/index.js`、`plugin/client.js`）✅
- 仓库创建满 1 天（2026-10-26 创建）✅
- 有 `dsh-plugin` topic ✅
- 描述只讲功能，不带营销词 ✅
- MIT 许可证 ✅
- Windows 10/11；DSH `>= 0.2.1-rc.2`（实测 0.2.1-rc.3）✅

## 二、dsh.so 收录（可选）

1. 打开 <https://www.dsh.so/zh/submit/>
2. 粘贴 `https://github.com/JKL-3484/dsh-drive-manager`
3. 类型选 **dsh 插件**
4. 点“开始检查”，通过后点“提交到 dsh.so”

## 基本信息

| 字段 | 内容 |
|---|---|
| 插件名 | 磁盘分工管家 |
| 包名 / id | `dsh-drive-manager` |
| 版本 | `0.2.0` |
| 仓库 | https://github.com/JKL-3484/dsh-drive-manager |
| 许可证 | MIT |
| 平台 | Windows 10 / 11 |
| DSH 兼容 | `>= 0.2.1-rc.2` |
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

## 截图

- `docs/screenshots/overview.png`
- `docs/screenshots/filter-c.png`
- `docs/screenshots/filter-d.png`
- `docs/screenshots/downloads.png`
- `docs/screenshots/plan.png`
- `docs/screenshots/multi-drive.png`

## 审核说明

- 源码扫描：`plugin/index.js`、`plugin/client.js`；无硬编码密钥、无外联、无删除 API。
- 子进程：仅 `Get-CimInstance`、`reg query`、`explorer.exe`，详见 `SECURITY.md`。
- 权限：只读扫描；大目录按时间预算统计，显示 `≥` 表示部分统计。
