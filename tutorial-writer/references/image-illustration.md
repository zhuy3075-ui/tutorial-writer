# image-illustration.md — img2.0 教程插图生成与插入规范

这份规范用于在教程合适位置插入由 img2.0 生成的图片。图片不是装饰，而是帮助学员缓解学习压力、理解知识点、快速汇总关键内容。

## 一、插图定位

img2.0 生成图主要承担三类作用：

| 作用 | 适合位置 | 图片类型 |
|------|----------|----------|
| 缓解学习压力 | 连续复杂步骤后、难点解释前、章节过半处 | 轻量场景插画、鼓励型视觉 |
| 知识点演示 | 抽象概念第一次出现、复杂机制解释处 | 教学插画、类比图、示意图 |
| 阶段汇总 | 章节结尾、模块结尾、作业前 | 总结海报、知识卡片、流程汇总图 |

图片必须和上下文紧密相关。不能为了“好看”插入与本节无关的插画。

## 二、什么时候生成图片

满足以下任一条件时，考虑插入 img2.0 图片：

- 某一节连续解释超过 600 字，读者可能疲劳。
- 某个知识点靠文字解释不够直观，但又不适合用严格流程图/画板。
- 需要用生活类比帮助小白理解抽象概念。
- 章节结尾需要一张“一眼看懂”的总结卡。
- 课堂讲师需要停下来讲解或互动。

不适合生成图片的情况：

- 读者需要看真实界面位置：用截图。
- 需要表达严格流程、架构、层级、决策：优先用画板。
- 需要精确对比数据：用表格。
- 图片会打断操作步骤连续性。

## 三、插图规划格式

写正文前，先规划插图位：

```text
插图编号：IMG-01
插入位置：第 X 章 / 第 X 节 / 某段之后
上下文：前文讲了 ______，后文要进入 ______
教学目的：缓解压力 / 知识点演示 / 阶段汇总
图片类型：教学插画 / 类比图 / 总结卡 / 场景图
图片要表达的一句话：______
是否生成：是 / 否
不生成原因：______
```

## 四、img2.0 提示词规范

每张图都要单独写生成提示词。提示词必须保存到独立文档，和教程正文分开。

提示词格式：

```text
Image ID: IMG-01
Use case: scientific-educational
Asset type: Feishu tutorial inline illustration
Primary request: ______
Context before image: ______
Context after image: ______
Teaching purpose: ______
Subject: ______
Style/medium: clean educational illustration, friendly but professional
Composition/framing: 16:9 horizontal layout, clear focal point, readable at document width
Color palette: calm neutral background with 2-3 accent colors
Text in image: none unless explicitly required
Constraints: no logo, no watermark, no fake UI, no dense text, no misleading technical details
Avoid: decorative-only image, unrelated people, clutter, tiny labels
Insertion note: insert after ______
```

如果图片需要文字，必须把文字写得很短，并逐字给出：

```text
Text (verbatim): "生成 → 验证 → 修正"
```

默认不建议在图中放长中文，因为生成图中文字容易出错。长说明放在图下正文。

## 五、提示词文档

每个教程都要生成一份“生图提示词文档”，用于记录所有图片规划与最终提示词。

命名：

```text
[教程标题]-img2-prompts.md
```

文档结构：

```markdown
# [教程标题] img2.0 生图提示词

## 插图总览

| ID | 插入位置 | 教学目的 | 图片类型 | 是否生成 | 文件名 |
|----|----------|----------|----------|----------|--------|

## IMG-01

[完整提示词]

## IMG-02

[完整提示词]
```

如果最终上传到飞书，提示词文档也要作为独立飞书云文档或附件交付，便于后续重生成和迭代。

## 六、生成与保存

默认使用 Codex 内部图片生成能力（img2.0 / built-in image generation）。如果图片要插入飞书文档，必须保存到本地教程资产目录，再通过飞书 CLI 插入。

建议本地结构：

```text
assets/
  images/
    IMG-01.png
    IMG-02.png
  prompts/
    tutorial-img2-prompts.md
```

图片生成后必须检查：

- 是否和章节上下文一致。
- 是否真的帮助理解或放松。
- 是否没有错误文字、错乱 UI、无关元素。
- 是否适合飞书文档宽度阅读。
- 是否没有水印、logo、奇怪文字。

## 七、插入飞书文档

把图片插入飞书文档时，优先使用飞书文档媒体插入能力：

```bash
lark-cli docs +media-insert --api-version v2 --doc "<doc-url>" --file ./assets/images/IMG-01.png
```

插入位置应靠近它服务的段落：

- 知识点演示图：放在概念解释后、操作步骤前。
- 缓解压力图：放在难点结束后、下一节开始前。
- 汇总图：放在章节结尾、练习前。

如果当前 CLI 不支持精确插入位置，就先在正文中放占位说明：

```xml
<p>[插图位 IMG-01：这里插入“AI 像助教一样把任务拆成小步骤”的教学插画]</p>
```

创建文档后再用媒体插入或人工调整到占位附近。不能因为无法精确插入就省略图片规划。

## 八、图片与画板、截图的分工

| 类型 | 负责什么 | 是否可由 img2.0 生成 |
|------|----------|----------------------|
| 截图 | 真实界面、按钮位置、操作结果 | 否 |
| 画板 | 流程、架构、层级、决策、对比 | 通常否，优先用 Mermaid/SVG |
| img2.0 图片 | 类比、氛围缓冲、知识点演示、阶段总结 | 是 |

一篇教程中三者可以同时存在，但不能重复表达同一件事。

## 九、输出验收

完成教程前检查：

- [ ] 已判断哪些位置需要 img2.0 插图，哪些不需要。
- [ ] 每张图片都有明确教学目的。
- [ ] 每张图片都有上下文说明和插入位置。
- [ ] 已生成独立的 img2.0 提示词文档。
- [ ] 需要生成的图片已生成并保存到本地资产目录。
- [ ] 图片已插入飞书文档，或文档中有明确插图位。
- [ ] 图片没有替代截图或画板该承担的职责。
