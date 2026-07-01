# tutorial-writer 分发、部署与使用教程

这份教程面向准备把 `tutorial-writer` 分发给其他人使用的人。它不只说明“怎么安装”，还说明这个 skill 能做什么、适合谁、部署后如何验证、使用者应该怎样提需求，以及后续如何做版本更新。

## 1. 先理解它是什么

`tutorial-writer` 是一个 Codex Skill，用来把知识库、参考教程、项目经验、PDF、飞书文档或模糊教学想法，转成结构化教程。它的重点不是替你“拼材料”，而是让 Codex 先诊断需求、规划大纲、安排图文节奏，再根据场景生成飞书 `docx` 教程或提炼参考教程模板。

适合分发给这些人：

- 需要给学员写 AI 编程课讲义的老师。
- 经常把知识库整理成教程的内容负责人。
- 想把项目复盘写成公众号式实战文的人。
- 需要用飞书 CLI 批量创建或更新教程文档的人。
- 想学习优秀教程结构，并把它沉淀成模板的人。

不适合这些场景：

- 只想要一句话摘要。
- 不想做需求确认，也不想审查大纲。
- 不需要飞书格式，也不需要教程结构。
- 主题强依赖最新资料，但又不允许联网校准。
- 希望 skill 自动修改原知识库仓库。

## 2. 核心功能

### 2.1 项目级需求诊断

正式写教程前，skill 会先判断教程项目类型，再通过老师视角和产品经理视角梳理需求。

它会覆盖这些维度：

- 项目目标：最终交付什么成果。
- 学员画像：学员会什么、卡在哪里。
- 课程目标：学完后能独立完成什么。
- 内容边界：必须讲、简讲、不讲、需要联网确认的内容。
- 素材来源：知识库、飞书链接、截图、GitHub、README、PDF。
- 审美表达：公众号实战文、课程讲义、操作手册还是 Wiki。
- 图文互动：截图、画板、img2.0、高亮块、作业、打卡。
- 发布交付：单文档、多文档、Wiki、飞书 CLI、GitHub。
- 风险验收：版本、权限、版权、隐私、飞书能力限制。

### 2.2 可点击选项式流程

所有需要用户做选择的地方，都要求优先弹出带描述的选项，例如：

- 快速生成 / 标准诊断 / 深度访谈。
- 总结借鉴 / 混合复刻 / 一比一还原。
- 通过大纲 / 调整章节 / 改表达风格。
- 更新原飞书文档 / 另存副本 / 只输出修改建议。

如果当前 Codex 环境不支持真正的可点击选项，skill 会降级成带描述的编号选项，并停止等待用户回复。

### 2.3 全流程规范大纲审查

需求确认后，skill 不会直接写正文，而是先出一份可审查的大纲。

大纲会包含：

- 教程定位。
- 教程主线。
- H1/H2/H3/H4 章节结构。
- 每章前言。
- 每节知识点。
- 飞书块规划。
- 截图、画板、img2.0 图片规划。
- 作业与打卡。
- 部署、README、GitHub 接入。
- 风险与验收。

用户确认大纲后，才会进入正文、图片生成和飞书发布。

### 2.4 飞书 docx 创建与更新

默认交付是飞书云文档 `docx`，不是普通 Markdown 文件。

常见行为：

- 没有原文档时：创建新的飞书 `docx`。
- 用户提供已有 `docx` 链接时：默认更新原文档。
- 用户要求新建副本时：才另建新链接。
- 更新已有文档时：优先使用精确块更新，不默认全文覆盖。

### 2.5 参考飞书教程处理

当用户提供优秀飞书教程链接时，skill 会先让用户选择处理方式：

- 总结借鉴：只学习结构、排版和图文节奏。
- 混合复刻：保留类似版式和图片位置，但正文换成本次主题。
- 一比一还原：复制原文、原图和格式，必须先确认权限。

没有权限确认时，不会复制大段原文或原图。

### 2.6 参考教程学习模式

如果用户目标是“学习优秀教程结构”“分析教程设计”“提炼模板”“优化这个 skill”，会进入参考教程学习模式。

这个模式不会创建飞书文档，而是输出：

- 结构卡。
- 节奏卡。
- 模板卡。
- 问题卡。
- 可复用教程模板。

适合用来研究别人教程为什么好，再把方法沉淀进自己的教程生产流程。

### 2.7 图文资产与 img2.0 插图

skill 会规划截图、画板和 img2.0 图片。

要求很明确：

- 图片必须服务具体教学问题。
- 不能生成泛泛概念图。
- 图片数量要和教程长度匹配。
- 如果规划了 img2.0 图片，就要在制作过程中生成、自检、插入文档。
- 生图提示词要单独沉淀，方便追溯。

### 2.8 作业、打卡与进度

教程里的作业不只是普通文字。

推荐方式：

- 文档内 `checkbox` 做学习引导。
- 作业区用高亮块、任务清单或表格呈现。
- 真实个人进度用飞书 Base / 表单 / 表格统计。
- 单人学习可复制一份个人教程副本后自行勾选。

## 3. 分发前准备

分发前，建议确认三件事。

### 3.1 选择分发来源

当前有两个 GitHub 来源：

- 独立仓库：[zhuy3075-ui/tutorial-writer](https://github.com/zhuy3075-ui/tutorial-writer)
- skills 聚合仓库：[zhuy3075-ui/skills](https://github.com/zhuy3075-ui/skills)

推荐给普通使用者使用独立仓库，路径更短，安装更清楚。

推荐给内部维护者使用聚合仓库，方便和其他 skill 一起管理。

### 3.2 检查本地目录结构

一个完整的 `tutorial-writer` 至少包含：

```text
tutorial-writer/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── choice-interaction.md
│   ├── intake-and-mode.md
│   ├── needs-diagnosis.md
│   ├── outline-review.md
│   ├── feishu-format.md
│   ├── image-illustration.md
│   ├── tutorial-analysis-mode.md
│   └── ...
└── reference-analysis/
    └── 2026-07-01-tutorial-template-study/
```

不要只复制 `SKILL.md`。这个 skill 大量规则放在 `references/` 里，少文件会导致行为断链。

### 3.3 不要分发敏感信息

分发前确认没有包含：

- `.env`
- API key
- 飞书 token
- 个人账号 Cookie
- 内部未授权材料
- 学员隐私数据

参考分析里的图片和 PDF 是教程结构研究材料；如果要对外公开分发，请确认这些材料是否适合公开。

## 4. 部署方式一：从独立仓库安装

适合普通使用者。

```bash
cd ~/Downloads
git clone https://github.com/zhuy3075-ui/tutorial-writer.git
mkdir -p ~/.codex/skills
rsync -a --delete tutorial-writer/tutorial-writer/ ~/.codex/skills/tutorial-writer/
```

检查是否安装成功：

```bash
ls ~/.codex/skills/tutorial-writer/SKILL.md
ls ~/.codex/skills/tutorial-writer/references
```

然后重启 Codex，或新建一个 Codex 对话。

## 5. 部署方式二：从 skills 聚合仓库安装

适合已经在维护整套 skill 的人。

```bash
cd ~/Downloads
git clone https://github.com/zhuy3075-ui/skills.git
mkdir -p ~/.codex/skills
rsync -a --delete "skills/10-Skill-Prompt-项目工程化/tutorial-writer/" ~/.codex/skills/tutorial-writer/
```

检查安装结果：

```bash
ls ~/.codex/skills/tutorial-writer/SKILL.md
```

如果路径里有中文目录，命令中要加引号。

## 6. 部署方式三：本地同步给同事

适合同一个团队里手动分发。

打包前先在维护者机器上确认：

```bash
cd /Users/zy/Documents/教程skill
git status --short
```

如果只想分发 skill 本体，可以打包这个目录：

```bash
cd /Users/zy/Documents/教程skill
zip -r tutorial-writer-skill.zip tutorial-writer -x "*/.DS_Store"
```

同事解压后安装：

```bash
mkdir -p ~/.codex/skills
rsync -a --delete tutorial-writer/ ~/.codex/skills/tutorial-writer/
```

## 7. 飞书 CLI 准备

如果使用者只分析教程结构，可以不配置飞书 CLI。

如果要生成或更新飞书 `docx`，必须确认 `lark-cli` 可用：

```bash
lark-cli docs --api-version v2 --help
lark-cli docs +create --api-version v2 --help
lark-cli docs +update --api-version v2 --help
```

常用创建命令：

```bash
lark-cli docs +create --api-version v2 --content @tutorial.xml --json
```

常用验证命令：

```bash
lark-cli docs +fetch --api-version v2 --doc "<飞书文档链接>" --doc-format xml --scope full --json
```

如果使用者没有飞书权限，可以在提示词里明确说：

```text
只生成本地草稿，不调用飞书 CLI，不上传飞书。
```

否则 skill 默认会把正式教程发布成飞书 `docx`。

## 8. 使用方式一：生成新教程

推荐新建一个 Codex 对话，然后这样说：

```text
请使用 $tutorial-writer，帮我生成一份飞书教程。

主题：Vibe Coding 小白入门
知识库路径：/Users/xxx/知识库
目标学员：用过 AI 写代码，但不会拆任务、不会判断输出质量的新手
预期成果：一份适合线下课使用的飞书 docx 教程

请先做需求诊断和全流程规范大纲，不要直接写正文。
```

正常流程：

```text
模式选择
→ 项目类型判断
→ 项目级需求诊断
→ 用户确认需求
→ 全流程规范大纲
→ 用户审查大纲
→ 正文生成
→ 图文资产生成
→ 飞书 CLI 发布
→ fetch 验证
```

## 9. 使用方式二：分析优秀教程结构

当你不是要生成教程，而是想学习一个优秀教程怎么写，可以这样说：

```text
请使用 $tutorial-writer 的参考教程学习模式，分析这个教程的结构。

参考材料：这里放飞书链接、PDF 路径或截图
目标：提炼可复用的教程模板，不要创建飞书文档，不要一比一复刻。

请区分“明确呈现”和“推断判断”，输出结构卡、节奏卡、模板卡和问题卡。
```

这个模式适合：

- 学习别人教程的目录结构。
- 分析图文节奏。
- 提炼可复用模板。
- 反向优化 `tutorial-writer`。

## 10. 使用方式三：参考飞书教程改写

如果用户提供一篇优秀飞书教程，希望借鉴或复刻：

```text
请使用 $tutorial-writer，参考这个飞书教程生成我的新教程。

参考链接：<飞书链接>
我的主题：____
目标读者：____

请先让我选择总结借鉴、混合复刻还是一比一还原。
```

注意：

- 总结借鉴不复制原文原图。
- 混合复刻保留类似结构，但内容换成本次主题。
- 一比一还原需要用户确认复制、复刻或课堂使用权限。

## 11. 使用方式四：更新已有飞书文档

如果已经有飞书 `docx`：

```text
请使用 $tutorial-writer 修改这个飞书文档，不要新建链接。

原文档：<docx 链接>
修改目标：
1. 补充需求诊断章节
2. 优化第 3 章图文衔接
3. 增加作业 checkbox

请先 fetch 原文档，再给修改目标诊断，确认后更新原链接。
```

skill 默认会走 `docs +update`，不会随便新建文档。

## 12. 使用方式五：只做本地草稿

有时使用者不想连飞书，只想先看内容：

```text
请使用 $tutorial-writer 生成本地教程草稿。

不要调用飞书 CLI，不要上传飞书。
输出 Markdown 草稿和图文规划即可。
```

这样可以先审内容，再决定是否发布到飞书。

## 13. 更新版本

### 13.1 从独立仓库更新

```bash
cd ~/Downloads/tutorial-writer
git pull
rsync -a --delete tutorial-writer/ ~/.codex/skills/tutorial-writer/
```

### 13.2 从聚合仓库更新

```bash
cd ~/Downloads/skills
git pull
rsync -a --delete "10-Skill-Prompt-项目工程化/tutorial-writer/" ~/.codex/skills/tutorial-writer/
```

### 13.3 检查安装版是否一致

```bash
diff -qr tutorial-writer ~/.codex/skills/tutorial-writer
```

如果从聚合仓库更新：

```bash
diff -qr "10-Skill-Prompt-项目工程化/tutorial-writer" ~/.codex/skills/tutorial-writer
```

## 14. 维护者版本管理

维护者建议同时维护两处：

- `zhuy3075-ui/tutorial-writer`：独立分发源。
- `zhuy3075-ui/skills`：聚合分发源。

更新顺序建议：

```text
1. 先更新 /Users/zy/Documents/教程skill/tutorial-writer
2. 同步到 ~/.codex/skills/tutorial-writer
3. 同步到 /Users/zy/Desktop/skills/10-Skill-Prompt-项目工程化/tutorial-writer
4. 分别运行静态检查
5. 分别提交和推送两个仓库
6. 更新 CODEBRAIN 交接记录
```

同步命令参考：

```bash
rsync -a --delete --exclude ".DS_Store" \
  /Users/zy/Documents/教程skill/tutorial-writer/ \
  /Users/zy/.codex/skills/tutorial-writer/

rsync -a --delete --exclude ".DS_Store" \
  /Users/zy/Documents/教程skill/tutorial-writer/ \
  "/Users/zy/Desktop/skills/10-Skill-Prompt-项目工程化/tutorial-writer/"
```

## 15. 分发验收清单

交给别人前，维护者检查：

- [ ] `SKILL.md` 存在。
- [ ] `agents/openai.yaml` 存在。
- [ ] `references/` 文件完整。
- [ ] `choice-interaction.md`、`intake-and-mode.md`、`needs-diagnosis.md`、`outline-review.md` 存在。
- [ ] `tutorial-analysis-mode.md` 存在。
- [ ] 没有 `.env`、token、Cookie、账号凭据。
- [ ] README 或分发教程说明了安装路径。
- [ ] 使用者知道是否需要 `lark-cli`。
- [ ] 使用者知道如何只生成本地草稿。
- [ ] 使用者知道如何更新版本。

## 16. 常见问题

### Q1：安装后 Codex 没触发 skill？

先检查目录：

```bash
ls ~/.codex/skills/tutorial-writer/SKILL.md
```

然后新建对话，用明确触发语：

```text
请使用 $tutorial-writer 生成一份教程。
```

### Q2：为什么一开始不直接写正文？

因为这个 skill 默认走需求诊断和大纲审查。这样能避免教程生硬、内容拼贴、图片无关、飞书格式不好看。

如果只是测试，可以明确说：

```text
这是一次快速测试，跳过需求诊断和大纲审查，只生成草稿，并标注质量风险。
```

### Q3：没有飞书权限怎么办？

可以只生成本地草稿，不调用飞书 CLI。

如果要发布到飞书，必须先解决 `lark-cli` 登录和文档权限。

### Q4：为什么没有弹出可点击选项？

可点击选项取决于当前 Codex 运行环境是否支持对应交互。环境不支持时，skill 会用带描述的编号选项降级，并等待用户回复。

### Q5：可以只分发 `SKILL.md` 吗？

不建议。这个 skill 的关键规则在 `references/` 里，只分发 `SKILL.md` 会导致功能缺失。

### Q6：PDF 和 reference-analysis 必须分发吗？

如果只想使用教程生成功能，可以不依赖参考分析资产。

如果希望保留“参考教程学习模式”的案例证据和模板来源，建议一起分发。对外公开前请确认 PDF 和样例图的授权边界。

## 17. 推荐给使用者的第一条消息

可以把这段直接发给新使用者：

```text
请使用 $tutorial-writer 帮我做一份教程。

我的主题：____
目标读者：____
知识库或素材路径：____
最终成果：飞书 docx / 本地草稿 / Wiki 课程 / 参考教程结构分析

请先通过可点击选项或编号选项确认模式，再做需求诊断和大纲审查。大纲确认前不要生成正文。
```

这条消息能让新用户快速进入正确流程。
