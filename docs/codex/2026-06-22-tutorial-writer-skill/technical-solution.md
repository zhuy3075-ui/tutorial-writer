# 教程课本 Skill 技术方案

## 方案概述

采用最小 Skill 结构：一个主 `SKILL.md` 承载触发描述和核心工作流，四份 reference 文档承载详细写作、截图、结构和飞书排版规则。当前阶段不引入脚本、不接飞书 API、不做自动截图。

这个方案符合 YAGNI 和 KISS：当前主要风险是内容生成质量不稳定，不是确定性程序逻辑缺失。先用清晰 reference 和真实样例试跑验证，比提前写校验脚本更稳。

## 当前目录结构

当前 `tutorial-writer/` 已整理为以下结构：

```text
tutorial-writer/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── writing-rules.md
    ├── screenshot-guide.md
    ├── tutorial-structure.md
    └── feishu-format.md
```

当前 `SKILL.md` 已写明需要加载 `references/writing-rules.md` 等路径。后续维护时不要再移动这四份 reference 文件；如果确实调整目录，必须同步更新 `SKILL.md` 的引用路径。

## 文件责任边界

### `SKILL.md`

负责放置：

- YAML frontmatter：`name` 和 `description`。
- Skill 的一句话定位。
- 核心工作流。
- 四段式展开规则。
- 需要加载哪些 reference，以及什么时候加载。
- 读者基线。
- 输出前检查清单。

不负责放置：

- 完整 26 条写作铁律。
- 三种教程骨架全文。
- 详细截图标注规范。
- 飞书排版细则。

### `agents/openai.yaml`

负责 UI 元数据：

- `display_name`：Skill 列表中显示的名称。
- `short_description`：Skill 列表中的短说明。
- `default_prompt`：显式包含 `$tutorial-writer` 的默认调用提示。

### `references/writing-rules.md`

负责语言和内容伦理规则：

- 零术语起步。
- 先例子后定义。
- 用“你”说话。
- 禁用俯视语言。
- 核心步骤全给。
- 不切篇、不埋收费伏笔。
- 课堂练习和讨论节点要求。

### `references/tutorial-structure.md`

负责三种教程骨架：

- 操作指南型。
- 概念讲解型。
- 案例拆解型。
- 骨架选择决策树。

### `references/screenshot-guide.md`

负责截图策略：

- 什么时候必须截图。
- 三种必须截图的场景。
- 红框、数字序号、箭头三种标注元素。
- 配图位标注格式。
- 不使用 GIF。

### `references/feishu-format.md`

负责飞书结构和排版：

- Callout、表格、代码块、折叠块四件套。
- 标题层级。
- 分隔线使用规则。
- 场外文档引用格式。
- 排版反模式。

## Progressive Disclosure 策略

`SKILL.md` 应保持短而可执行，只让执行 agent 先看到完整主流程。详细规则按任务阶段加载：

| 阶段 | 应加载 reference | 目的 |
|---|---|---|
| 选教程结构 | `tutorial-structure.md` | 从三种骨架中选一种。 |
| 改写语言 | `writing-rules.md` | 把知识库内容改成课堂可懂的教程语言。 |
| 标注配图位 | `screenshot-guide.md` | 判断哪里要图、图里标什么。 |
| 输出飞书草稿 | `feishu-format.md` | 确保排版结构完整、元素使用正确。 |

不要把 reference 内容复制进 `SKILL.md`。同一条规则只保留在一个地方，避免后续更新时出现两套版本。

## Skill 规范差异

当前 `tutorial-writer/SKILL.md` frontmatter 包含：

```yaml
name: tutorial-writer
description: ...
```

根据 Skill Creator 规范，frontmatter 应只包含 `name` 和 `description`。当前已符合该要求。

## 校验方案

### 结构校验

后续整理 Skill 后运行基础校验：

```bash
python /Users/zy/.codex/skills/.system/skill-creator/scripts/quick_validate.py /Users/zy/Documents/教程skill/tutorial-writer
```

如果本地该脚本路径不存在，应先在 Skill Creator 安装目录中查找 `quick_validate.py`，再运行同等校验。校验失败时只修复报告的 Skill 结构问题，不顺手重写内容。

### 人工样例验证

至少选择 3 个教程主题试跑：

1. 一个操作指南型主题，例如“用 Codex 创建一个本地 Skill”。
2. 一个概念讲解型主题，例如“为什么 Skill 要做 progressive disclosure”。
3. 一个案例拆解型主题，例如“一个教程为什么从能看变成能上课”。

每篇输出后检查：

- 是否选择了正确骨架。
- 是否包含四段式展开。
- 是否有配图位、练习、讨论节点、来源引用。
- 是否符合飞书排版四件套。
- 是否没有俯视语言、收费伏笔和空泛作业。

### 不引入脚本的理由

当前规则大多依赖语义判断，例如“是否俯视读者”“是否来自真实踩坑”“练习是否能课堂验证”。这些判断不适合第一轮就用脚本硬判。等 3 篇试跑后，如果发现稳定、机械、重复的检查项，再考虑新增脚本。

## 迭代边界

第一轮只做：

- 修正目录结构或引用路径。
- 精简 `SKILL.md`。
- 保持 4 份 reference 文档职责清晰。
- 试跑 3 篇教程并记录问题。

第一轮不做：

- 飞书 API 发布。
- 自动截图生成。
- 自动评分系统。
- 多受众版本切换。
- 通用 Skill 制作模板。
