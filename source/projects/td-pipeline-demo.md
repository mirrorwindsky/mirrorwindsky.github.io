---
layout: page
title: TD Pipeline Demo｜Python 配置工具与 Unity 玩法验证
date: 2026-09-12 18:00:00
updated: 2026-09-15
description: 技术策划个人作品：支持图形界面、自定义校验规则、批量调参和 AI 规则提案的 Python 配置工具，配套 Unity 可玩 Demo。
permalink: projects/td-pipeline-demo/
comments: false
aside: false
top_img: false
---

## TD Pipeline Demo

**面向策划的 Python 配置工具，配套 Unity 可玩 Demo。**

围绕配置检查、校验标准调整和重复调参，制作支持图形界面、自定义规则、批量更新与 AI 辅助编写规则的桌面工具，并通过 Unity 玩法验证配置修改的实际效果。

**[GitHub 源码](https://github.com/mirrorwindsky/TD-Pipeline-Demo)** · **[工具使用说明](https://github.com/mirrorwindsky/TD-Pipeline-Demo/blob/main/Docs/%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E.md)** · **[下载游戏demo与配置工具](https://github.com/mirrorwindsky/TD-Pipeline-Demo/releases/download/v1.0.0%2Btool/demo.zip)**

## 演示视频

<!-- 将演示视频放到 source/video/td-pipeline-demo.mp4 -->
<!-- markdownlint-disable MD033 -->

<div style="margin: 24px 0;">
  <video
    controls
    preload="metadata"
    playsinline
    style="width: 100%; max-width: 960px; border-radius: 8px; display: block; margin: 0 auto;"
  >
    <source src="/video/td-pipeline-demo.mp4" type="video/mp4">
    当前浏览器不支持 HTML5 视频播放。
  </video>
</div>

<!-- markdownlint-enable MD033 -->

## Python 配置工具 V3

| 功能 | 已实现能力 | 使用价值 |
| --- | --- | --- |
| **桌面图形界面** | 中文 / 英文切换，在窗口中完成规则编辑、校验、生成和批量操作 | 降低命令行使用门槛 |
| **自定义校验标准** | 表单设置必需列、必填值、类型、数值范围、允许值、唯一值、正则、跨表与指定场景引用；支持新增、编辑、复制、启停和删除规则 | 调整已有规则类型的检查标准，无需修改 Python 代码 |
| **规则草稿与保存** | 草稿可直接用于校验、生成与批量操作；支持保存、重新加载，并在保存前检查规则文件是否被外部修改 | 先试验规则效果，再决定是否保存 |
| **多表检查与错误定位** | 检查物品、任务目标、交互物配置，展示问题所在表、行号、字段、规则与说明，区分错误和警告 | 快速定位缺值、重复 ID、类型错误及失效引用 |
| **批量调参** | 根据更新表预览交互次数的修改前后值；应用前校验全部修改后数据，通过后写回 CSV | 减少逐条修改，批量操作遵循同一套校验标准 |
| **AI 辅助编写规则** | 接入 OpenAI / DeepSeek，将自然语言需求转为规则新增、更新或停用提案；预览差异、确认应用到草稿后，由本地引擎校验 | 降低规则编写门槛，保留人工确认与本地检查 |
| **数据生成与错误拦截** | 生成 Unity 使用的交互物与任务目标 JSON；校验错误阻止生成和批量写入，保留原文件，警告允许继续 | 在配置进入游戏前发现问题，避免错误配置覆盖已有数据 |
| **可选 AI 与密钥管理** | 常规功能无需 AI 账号；提供固定规则的离线演示，支持会话密钥及 Windows 凭据管理器保存 / 移除密钥 | 无 AI 服务也能使用核心工具，密钥不写入项目文件 |
| **Windows EXE 打包** | 提供打包脚本；构建后的独立 EXE 自带 Python 与 tkinter，支持查找或选择项目目录 | 便于交付给未安装 Python 的使用者 |

CSV 内容由 Excel 等表格软件编辑；批量应用写回 CSV 后，需再点击生成 JSON。AI 接收需求、表头和当前规则，不发送 CSV 数据行。

## Unity 玩法验证

配套第三人称工业设施 Demo，包含物品拾取、设备修复、终端激活、出口解锁和任务完成，以及交互提示、目标 HUD 与最小背包状态。

已验证将设备交互次数从 3 改为 1 并重新生成数据后，游戏中的完成条件同步改变；引用不存在的物品 ID 时，工具会阻止生成并保留上一版输出。可玩版本已完成从启动到 Mission Complete 的人工测试。

## 项目迭代与验证

根据从业者反馈，将命令行工具扩展为 GUI、可编辑校验标准与 AI 规则提案。使用 **40 条内容记录、8 条批量更新**的复用样例开展 QA，修复过场景引用漏检和异常 CSV 静默截断两个实际问题；V3 补充了规则、草稿、GUI、AI 接口、凭据与 EXE 项目定位测试。

技术栈：**Python / tkinter / ttk、CSV / JSON、Unity 6.3 LTS / C#、Git / GitHub**。个人技术策划作品，AI / Codex 辅助实现与调试。

[技术实现](https://github.com/mirrorwindsky/TD-Pipeline-Demo/blob/main/Docs/%E6%8A%80%E6%9C%AF%E5%AE%9E%E7%8E%B0.md) · [项目案例](https://github.com/mirrorwindsky/TD-Pipeline-Demo/blob/main/Docs/Pipeline_Case_Study.zh-CN.md) · [QA 记录](https://github.com/mirrorwindsky/TD-Pipeline-Demo/blob/main/Docs/D11_QA.zh-CN.md) · [中文 README](https://github.com/mirrorwindsky/TD-Pipeline-Demo/blob/main/README.zh-CN.md) / [English](https://github.com/mirrorwindsky/TD-Pipeline-Demo/blob/main/README.md)
