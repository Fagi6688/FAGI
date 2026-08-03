# FAGI 小红书生态融合智能体

> **F**usion **A**gent **G**roup **I**ntelligence — 七位专家 agent 协作的小红书经营工具箱

FAGI 是小红书生态经营体系的统一入口。你不需要记住七个工具的名字，只需要把需求告诉 FAGI，它会自动路由到最合适的专家，完成后推荐下一步。

## 核心特性

- 🎯 **单入口路由**：用户只对 FAGI 说话，FAGI 自动识别意图并路由到最合适的专家
- 🔄 **完整闭环**：研究 → 规划 → 创作 → 审查 → 复盘，覆盖小红书经营全流程
- 🤝 **多 agent 协作**：七位专家各有专长，FAGI 负责协调衔接和结果流转
- 🧭 **动态导航**：每步完成后根据实际结论推荐下一步，不预设固定流程
- 🆕 **新手友好**：第一次使用有完整教程，用任务语言描述能力，不展示技术细节

## 七位专家 + 更新器

| 专家 | 擅长 | 闭环位置 |
|---|---|---|
| **关键词研究员** | 10 维关键词矩阵 + 搜索量验证 + 账号阶段部署策略 | 研究 |
| **双账号策略师** | 双账号定位 + 月度 12 条选题 + 三阶段节奏 + 跨月迭代 | 规划 |
| **标题优化师** | 8 种框架 + 75 个爆款公式库 + ≤20 字标题 + 张力检查 | 创作 |
| **笔记作家** | 5 篇完整笔记 + AI 味修正 + 关键词密度 + 合规自检 | 创作 |
| **合规检测官** | 小红书违禁词 9 大章节 + 广告法增补 + 评分 + OCR | 审查 |
| **发布前审查官** | 多平台（抖音/小红书/视频号）审稿 + 保意修复 + 个人规则库 | 审查 |
| **数据复盘师** | 漏斗四层诊断 + 加码/砍掉判断 + 数据仪表盘 | 复盘 |
| **更新器** | 从 GitHub 同步最新 FAGI，保留用户个人数据 | 维护 |

## 快速开始

### 安装

将本仓库下载或 clone 到本地，然后把 `skills/` 目录下的内容复制到你的 WorkBuddy 项目中：

```bash
# 方式一：clone 仓库
git clone https://github.com/your-username/fagi.git

# 方式二：下载 zip 后解压
unzip fagi.zip
```

### 目录结构

```
fagi/
├── SKILL.md                          # FAGI 主入口（路由器 + 导航器）
├── fagi-xhs-keyword-planner/         # 关键词研究员
│   ├── SKILL.md
│   └── scripts/
├── fagi-xhs-dual-account-strategist/  # 双账号策略师
│   ├── SKILL.md
│   ├── scripts/
│   ├── references/
│   └── data/
├── fagi-xhs-title-optimizer/          # 标题优化师
│   └── SKILL.md
├── fagi-xhs-note-writer/             # 笔记作家
│   └── SKILL.md
├── fagi-xhs-compliance-check/        # 合规检测官
│   ├── SKILL.md
│   └── scripts/
├── fagi-publish-precheck/       # 发布前审查官
│   ├── SKILL.md
│   ├── scripts/
│   ├── references/
│   ├── templates/
│   └── data/
├── fagi-xhs-data-review/             # 数据复盘师
│   └── SKILL.md
├── fagi-update/                      # 更新器（从 GitHub 同步最新 FAGI）
│   └── SKILL.md
├── LICENSE                           # MIT
├── README.md                         # 本文件
├── .gitignore
└── package.json
```

### 在 WorkBuddy 中使用

1. 把上述 skill 目录复制到你项目的 `skills/` 目录下
2. 在 `.workbuddy/skills/` 下创建符号链接（或直接复制）
3. 在对话中输入 `/fagi` 或直接描述你的小红书需求

```bash
# 示例：创建符号链接加载点
ln -sfn /path/to/your/project/skills/fagi /path/to/your/project/.workbuddy/skills/fagi
ln -sfn /path/to/your/project/skills/fagi-xhs-keyword-planner /path/to/your/project/.workbuddy/skills/fagi-xhs-keyword-planner
# ... 其余 6 个子 skill + fagi-update 同理
```

## 使用方式

### 触发 FAGI

输入 `/fagi` 或直接说你的需求。第一次使用输入 `/fagi 新手入门`。

### 典型场景

**从 0 起号：**

```
用户：我在做功效护肤，小红书刚起步，不知道发什么
  → 关键词研究员：做 10 维关键词矩阵
  → 双账号策略师：基于关键词做月度选题
  → 标题优化师：给选题起标题
  → 笔记作家：写 5 篇笔记
  → 合规检测官：发布前合规检查
  → 发布后 → 数据复盘师：复盘优化
```

**已有内容要发布：**

```
用户：这段文案能不能发小红书？
  → 合规检测官：小红书违禁词检测 + 评分
  → 发布前审查官：保意修复（如需改稿）
```

**数据不好要优化：**

```
用户：最近 3 篇笔记数据都不好
  → 数据复盘师：漏斗四层诊断
  → 根据结论路由到 标题优化师 / 笔记作家 / 关键词研究员
```

## 架构设计

### 三模式架构（参照 dbskill）

- **模式 C 新手教程**：第一次使用时介绍能力，带用户完成首次实际使用
- **模式 A 任务前路由**：识别用户意图，路由到最合适的专家
- **模式 B 任务后导航**：根据上一位专家的结论，推荐当前最值得处理的下一步

### 单步路由原则

每次只决定当前一位专家。不预设「先 A 再 B 再 C」的长链，因为实际结果可能改变方向。FAGI 的导航地图定义了每种结论下的推荐下一步，但最终路由由当前对话上下文决定。

### 两位审查官的区分

合规检测官和发布前审查官都做合规检查，但定位不同：

| 场景 | 路由到 | 理由 |
|---|---|---|
| 只发小红书 + 要评分 + OCR | 合规检测官 | 9 大章节 + 评分 + OCR 是专长 |
| 多平台发布 | 发布前审查官 | 多平台规则差异逐平台给结论 |
| 要可直接替换的修复稿 | 发布前审查官 | 保意修复是核心能力 |
| 已被限流要复盘归因 | 发布前审查官 | 有 diagnose 流程和个人规则沉淀 |
| 想长期积累行业敏感词 | 发布前审查官 | `data/` 个人规则库越用越准 |
| 起步阶段快速过一遍违禁词 | 合规检测官 | 更轻量，输出更结构化 |

## 技术栈

- **运行环境**：WorkBuddy（支持 Skill 机制的 AI 助手平台）
- **脚本语言**：Python 3（关键词研究员、双账号策略师、合规检测官、发布前审查官的数据处理脚本）
- **数据格式**：Markdown + Excel（.xlsx）
- **架构参考**：[dbskill](https://github.com/dontbesilent2025/dbskill)（dontbesilent 商业工具箱）的三模式路由 + 导航地图设计

## 子 skill 说明

| skill 目录 | 角色名 | 核心能力 |
|---|---|---|
| `fagi-xhs-keyword-planner` | 关键词研究员 | 10 维关键词矩阵 + DSO100 搜索量验证 + 账号阶段部署策略 |
| `fagi-xhs-dual-account-strategist` | 双账号策略师 | 3 轮对话 + 双账号策略 + 12 条月度选题 + Excel 导出 |
| `fagi-xhs-title-optimizer` | 标题优化师 | 8 框架首轮 + 75 公式库重试 + Top 3 推荐 |
| `fagi-xhs-note-writer` | 笔记作家 | 5 篇笔记 + 6 类 AI 味清洗 + 关键词密度 + 合规自检 |
| `fagi-xhs-compliance-check` | 合规检测官 | 9 大章节违禁词 + 广告法增补 + 评分 + OCR 图片识别 |
| `fagi-publish-precheck` | 发布前审查官 | 多平台逐条判定 + 保意修复 + 个人规则库沉淀 |
| `fagi-xhs-data-review` | 数据复盘师 | 漏斗四层诊断 + 加码/砍掉判断 + HTML 数据仪表盘 |
| `fagi-update` | 更新器 | 从 GitHub 同步最新 FAGI，保留用户个人数据 |

## 许可证

[MIT License](./LICENSE)

各子 skill 保留各自的许可证声明。如子 skill 未单独声明，适用本仓库的 MIT 许可证。

## 贡献

欢迎提交 Issue 和 PR。提交前请阅读 [CONTRIBUTING](#)（如有）。

## 致谢

- **架构参考**：[dbskill](https://github.com/dontbesilent2025/dbskill) — dontbesilent 商业工具箱
- **子 skill 来源**：小红书生态专家团 7 个独立 skill 包
- **命名释义**：FAGI = Fusion Agent Group Intelligence（融合智能体群）
