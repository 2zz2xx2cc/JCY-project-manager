# JCY Project Manager
改造自插件 [](https://community.obsidian.md/plugins/project-manager),自己使用过程中微调修改，去除一些bug，当前整体变化不大。

一款为 [Obsidian](https://obsidian.md) 打造的全功能项目管理插件，提供甘特图、看板、表格三种视图，让你的项目计划和任务管理完全融入笔记工作流。

---

## 功能特性

### 多视图切换

| 视图 | 适用场景 |
|------|----------|
| **表格视图** | 快速浏览、批量操作、按字段排序筛选 |
| **甘特图** | 时间线规划、依赖关系可视化、进度跟踪 |
| **看板视图** | 按状态分列管理、拖拽流转任务 |

### 任务管理

- **丰富的任务属性**：状态、优先级、开始时间、截止时间、进度条、执行人、标签、描述
- **子任务**：支持多层级嵌套子任务
- **任务依赖**：为任务设置前置依赖，甘特图中可视化依赖箭头
- **循环任务**：支持按周期自动生成重复任务
- **时间追踪**：记录预估工时与实际工时日志

### 甘特图

- 粒度切换：天 / 周 / 月 / 季度
- 拖拽调整任务时间范围
- 拖拽改变任务顺序
- 里程碑节点
- 今日基准线
- 依赖关系箭头连线

### 看板视图

- 按任务状态自动分列
- 拖拽卡片跨列流转
- 卡片内展示子任务数量、优先级色条、描述预览

### 项目配置

- 自定义项目图标（emoji）和颜色
- 自定义字段（Custom Fields）：文本、数字、日期、下拉选项等类型
- 团队成员管理
- 保存视图（Saved Views）：保存常用筛选/排序配置
- 任务筛选与搜索

### 通知与自动化

- **截止日期提醒**：提前 N 天推送桌面通知
- **自动调度**：关闭时自动保存任务

### 数据存储（Markdown 原生）

所有数据以 Markdown 文件形式存储，与 Obsidian 的双链笔记完全兼容：

```
内容/计划/
├── 项目A.md          # 项目文件（pm-project: true）
├── 项目A_tasks/
│   ├── 任务1.md      # 任务文件（pm-task: true）
│   └── 任务2.md
└── Projects.md       # 全局可读的项目概览
```

**项目文件示例：**

```yaml
---
pm-project: true
id: "r5tr1791mquorbdi"
title: "项目名称"
description: "项目描述"
color: "#b07d9e"
icon: "📝"
taskIds: ["task001", "task002"]
teamMembers: ["焦重阳"]
---
```

**任务文件示例：**

```yaml
---
pm-task: true
projectId: "r5tr1791mquorbdi"
id: "task001"
title: "任务标题"
status: "in-progress"
priority: "high"
start: "2026-06-01"
due: "2026-06-30"
progress: 60
assignees: ["焦重阳"]
tags: ["feature"]
subtaskIds: []
dependencies: []
---
```

---

## 安装

### 手动安装

1. 下载最新 Release 中的 `main.js`、`styles.css`、`manifest.json`
2. 将三个文件放入 Obsidian Vault 的 `.obsidian/plugins/JCY-project-manager/` 目录
3. 在 Obsidian「设置 → 第三方插件」中启用 **JCY Project Manager**

### 从 BRAT 安装（测试版）

1. 安装 [BRAT](https://github.com/TfTHacker/obsidian42-brat) 插件
2. 在 BRAT 设置中添加此仓库地址
3. 点击「Add Plugin」

---

## 快速上手

### 1. 配置项目目录

进入「设置 → JCY Project Manager」，设置 **Projects Folder**（存放项目文件的目录，默认为 `内容/计划`）。

### 2. 新建项目

点击左侧边栏的项目管理图标，进入项目列表，点击「New Project」创建项目。

### 3. 添加任务

在项目视图中，切换到「表格」或「甘特图」视图，点击底部的「+ Add Task」添加任务。

### 4. 切换视图

使用工具栏左上角的视图切换按钮在表格、甘特图、看板之间切换。

---

## 插件设置

| 设置项 | 说明 |
|--------|------|
| Projects Folder | 项目文件的存储目录 |
| Default View | 打开项目时的默认视图（table / gantt / kanban） |
| Gantt Granularity | 甘特图默认粒度（day / week / month / quarter） |
| Gantt Week Label | 周列表显示方式（weekNumber / date） |
| Statuses | 自定义任务状态列表（标签、颜色、图标、是否代表完成） |
| Priorities | 自定义优先级列表 |
| Global Team Members | 全局团队成员列表 |
| Notifications Enabled | 是否开启截止日期提醒 |
| Notification Lead Days | 提前几天触发提醒 |
| Auto Schedule | 关闭任务弹窗时自动保存 |
| Kanban Show Subtasks | 看板卡片是否显示子任务数量 |
| Kanban Show Description Preview | 看板卡片是否显示描述预览 |

### 默认状态配置

| 状态 ID | 标签 | 图标 | 含义 |
|---------|------|------|------|
| `todo` | 未开始 | `·` | 尚未开始 |
| `in-progress` | 处理中 | `-` | 正在进行 |
| `blocked` | 阻塞中 | `!` | 被阻塞，无法推进 |
| `discussing` | 讨论中 | `+` | 评审讨论阶段 |
| `on-hold` | 搁置中 | `/` | 暂时搁置 |
| `done` | 已完成 | `x` | 已完成（complete = true） |
| `deferred` | 已延期 | `>` | 计划推迟 |
| `planned` | 已计划 | `<` | 已排期尚未开始 |
| `cancelled` | 已取消 | `#` | 已取消（complete = true） |

---

## 数据兼容性

- 所有任务和项目均以纯 Markdown 文件存储，不依赖外部数据库
- 可通过 Git 对所有项目数据进行版本控制
- `Projects.md` 提供人类可读的项目树概览，便于快速检索

---

## 版本历史

| 版本 | 说明 |
|------|------|
| 1.6.3 | 当前版本 |

---

## 致谢

本插件基于 [Stepan Kropachev](https://github.com/StepanKropachev) 的原始项目开发，在其基础上进行了定制化修改，增加了中文状态支持、任务数据格式规范化等改进。

---

## License

MIT
