# 教程课本 Skill 执行计划

## 实施策略

按最小变更完善现有 `tutorial-writer` Skill：先确认结构和引用路径一致，再用真实教程主题验证效果。更复杂的替代方案是同时做脚本校验、飞书发布和通用模板，但这些不解决当前最核心的问题，且会增加维护成本。

本计划默认当前目录不是 git 仓库，因此验证以文件检查、Skill 基础校验和样例试跑为主。

## 文件职责

| 文件或目录 | 职责 |
|---|---|
| `tutorial-writer/SKILL.md` | Skill 入口、触发描述、主工作流、reference 导航、输出检查清单。 |
| `tutorial-writer/references/writing-rules.md` | 语言、结构、课堂交付和内容伦理规则。 |
| `tutorial-writer/references/tutorial-structure.md` | 三种教程骨架和选择规则。 |
| `tutorial-writer/references/screenshot-guide.md` | 截图时机、标注元素和配图位格式。 |
| `tutorial-writer/references/feishu-format.md` | 飞书排版元素、布局、标题层级和反模式。 |

## 执行步骤

### Step 1: 确认当前文件状态

操作：

```bash
find /Users/zy/Documents/教程skill -maxdepth 3 -type f -print | sort
```

验证：

- 能看到 `tutorial-writer/SKILL.md`。
- 能看到四份现有规则文档。
- 若已存在 `tutorial-writer/references/`，先检查是否已有同名文件，避免覆盖用户改动。

### Step 2: 确认 reference 目录结构

操作：

```bash
find /Users/zy/Documents/教程skill/tutorial-writer/references -maxdepth 1 -type f -print | sort
grep -n "references/" /Users/zy/Documents/教程skill/tutorial-writer/SKILL.md
```

验证：

```bash
test -f /Users/zy/Documents/教程skill/tutorial-writer/references/writing-rules.md
test -f /Users/zy/Documents/教程skill/tutorial-writer/references/screenshot-guide.md
test -f /Users/zy/Documents/教程skill/tutorial-writer/references/tutorial-structure.md
test -f /Users/zy/Documents/教程skill/tutorial-writer/references/feishu-format.md
```

预期：四条命令均退出码为 0。

### Step 3: 精简并校正 `SKILL.md`

操作：

- 保留 `name: tutorial-writer`。
- 保留并强化 `description`，让它包含用途和触发条件。
- 确认没有 `agent_created: true` 等非必要 frontmatter 字段。
- 确认 reference 路径均为 `references/*.md`。
- 保持主流程、四段式展开、读者基线和输出检查清单。

验证：

```bash
sed -n '1,80p' /Users/zy/Documents/教程skill/tutorial-writer/SKILL.md
grep -n "references/" /Users/zy/Documents/教程skill/tutorial-writer/SKILL.md
```

预期：

- frontmatter 只包含 `name` 和 `description`。
- 四份 reference 路径都能在 `SKILL.md` 中看到。

### Step 4: 运行 Skill 基础校验

操作：

```bash
python /Users/zy/.codex/skills/.system/skill-creator/scripts/quick_validate.py /Users/zy/Documents/教程skill/tutorial-writer
```

验证：

- 校验通过。
- 若脚本路径不存在，先用 `find /Users/zy/.codex/skills -name quick_validate.py -print` 定位脚本。
- 若校验失败，只修复校验报告中和 Skill 结构直接相关的问题。

### Step 5: 试跑 3 篇教程

操作：

用整理后的 Skill 分别生成三类教程草稿：

1. 操作指南型：“用 Codex 创建一个本地 Skill”。
2. 概念讲解型：“为什么 Skill 要做 progressive disclosure”。
3. 案例拆解型：“一个教程为什么从能看变成能上课”。

验证：

- 每篇都只选择一种骨架。
- 每篇都包含开头卡片、正文、练习、前置阅读和下一步。
- 每篇至少一个讨论节点。
- 每篇至少一个“我栽过的坑”。
- 操作型教程有关键步骤配图位。
- 概念型教程先例子后定义。
- 案例型教程包含失败尝试和可迁移表格。

### Step 6: 根据试跑结果小幅迭代

操作：

- 如果 3 篇都在同一类规则上失败，把对应规则写得更明确。
- 如果失败只发生在某个样例，不新增通用规则，先修样例提示或使用方式。
- 不新增脚本，除非失败项是稳定、机械、重复、可自动判断的。

验证：

- 重新生成失败类型的教程草稿。
- 确认原失败项已消失。
- 确认没有引入新骨架、新目录或新工具依赖。

## 工程约束

- YAGNI：不做飞书 API、自动截图、自动评分、多受众切换。
- KISS：能靠 reference 规则解决的，不引入脚本。
- 外科手术式修改：只改 `tutorial-writer/` 内和本 Skill 直接相关的文件。
- 高内聚：主流程留在 `SKILL.md`，细则留在对应 reference。
- 低耦合：不依赖外部服务，不把飞书发布流程塞进教程生成 Skill。
- Fail Fast：缺少教程主题或知识库素材时先问，不生成空泛草稿。

## 完成标准

- `tutorial-writer/` 目录结构与 `SKILL.md` 引用路径一致。
- `SKILL.md` 通过基础 Skill 校验。
- 三类教程各完成一次试跑。
- 试跑输出满足 `spec.md` 的验收清单。
- 最终报告列出实际改动文件、每个文件改动原因、验证命令和结果。
