---
layout: page
title: TD Pipeline Demo｜技术策划作品展示
date: 2026-09-12 18:00:00
permalink: projects/td-pipeline-demo/
comments: false
aside: false
top_img: false
---

# TD Pipeline Demo

一个面向 **Technical Designer / 技术策划** 方向制作的个人作品项目。

项目将一个完整可玩的 Unity Vertical Slice，与策划侧 CSV 配置、Python Content Pipeline、数据校验、Batch 自动化和 QA 验证连接在同一条工作流中。

<!-- 将演示视频放到 source/video/td-pipeline-demo.mp4 -->

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

## 项目入口

**[▶ 下载 Windows x64 可玩版本 v1.0.0](https://github.com/mirrorwindsky/TD-Pipeline-Demo/releases/download/v1.0.0/TD-Pipeline-Demo-Windows-x64-v1.0.0.zip)**

**[⌨ 查看 GitHub 源码](https://github.com/mirrorwindsky/TD-Pipeline-Demo)**

**[📦 查看 GitHub Release](https://github.com/mirrorwindsky/TD-Pipeline-Demo/releases/tag/v1.0.0)**

---

## 视频展示内容

这段演示主要展示三个部分。

### 1. 完整 Gameplay Vertical Slice

玩家需要完成：

```text
PowerCell Pickup
→ PowerNode Repair
→ ControlTerminal Activation
→ Exit Unlock
→ Mission Complete
```

Demo 包含第三人称移动与镜头、Pickup / Device / Gate 交互、Objective / HUD，以及一条完整的任务依赖链。

### 2. 配置驱动的玩法行为

PowerNode 的 `requiredInteractions` 等玩法参数来自策划侧 `interactables.csv`。

视频中将：

```text
requiredInteractions: 3 → 1
```

随后运行 Python Content Pipeline 重新生成数据。在不修改对应 C# Gameplay Code 的情况下，Unity Runtime 中的 PowerNode 从需要三次交互变为一次交互即可完成。

这段演示用于证明：**策划侧源数据的修改可以经过 Pipeline 真实传播到 Runtime 行为。**

### 3. Pipeline 错误拦截

随后将 PowerNode 的：

```text
requiredItemId: power_cell
```

故意修改为不存在的：

```text
requiredItemId: fake_cell
```

再次运行 Pipeline 时，Cross-Reference Validation 会检测到非法 Item 引用并阻止 Generation，避免错误数据覆盖上一版已经验证通过的合法输出。

---

## Content Pipeline

项目当前的核心内容流程：

```text
Designer-authored CSV
        ↓
Parse Once SourceTables
        ↓
Typed ContentModel
        ↓
Schema / Type / Range / Duplicate Validation
        ↓
Cross-Table Reference Validation
        ↓
Active Scene Config Reference Validation
        ↓
ERROR Gate
        ↓
Generated JSON
        ↓
Unity Runtime
```

Designer-facing CLI：

```powershell
py Tools/config_tool.py generate
py Tools/config_tool.py batch-preview
py Tools/config_tool.py batch-apply
```

其中：

- `generate`：正常校验并生成 Unity 消费的数据；
- `batch-preview`：完整校验 Batch，但不修改源数据；
- `batch-apply`：校验通过后批量修改源数据，并使用 atomic replacement 写回。

---

## QA 与量化

项目使用一套 **40-record Scale Fixture** 对 Pipeline 进行系统测试，覆盖：

- Schema / Missing Value
- Type / Range
- Duplicate ID
- Illegal `interactionType`
- Cross-Table Reference
- Active Scene Config Reference
- Empty / Malformed CSV
- Fail-Safe Output Preservation

QA 过程中实际发现并修复了 **2 个真实 Validation Bug**：

1. Active V2 Scene reference coverage gap；
2. Malformed CSV silent truncation。

在固定 8 条 `requiredInteractions` 修改的受控对比中：

```text
Manual execution:       192.000 s
Automated execution:      0.287 s
```

该数据仅表示 **execution-stage benchmark**，不包含 Batch Request 本身的编写时间，也不代表整个内容生产流程提升了同等倍率。

---

## 技术栈

- Unity 6.3 LTS
- C#
- Python
- CSV / JSON
- Git / GitHub

---

## 更多技术文档

**[Pipeline Case Study｜中文](https://github.com/mirrorwindsky/TD-Pipeline-Demo/blob/main/Docs/Pipeline_Case_Study.zh-CN.md)**

**[D11 QA + Scale Test｜中文](https://github.com/mirrorwindsky/TD-Pipeline-Demo/blob/main/Docs/D11_QA.zh-CN.md)**

完整源码、中英文技术文档，以及 Windows x64 standalone build 均已公开于 GitHub。
