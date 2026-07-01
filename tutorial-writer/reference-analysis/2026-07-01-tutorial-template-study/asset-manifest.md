# 参考教程资产清单

## 读取方式

- 飞书文档读取：`lark-cli docs +fetch --api-version v2 --as user`。
- 图片处理：先 `docs +media-download`，403 时改用 `docs +media-preview`。
- PDF 处理：`pdfinfo` 读取元数据，`pdftoppm` 渲染关键页。

## 文档结构统计

| 来源 | 字符数 | H1 | H2 | 图片 | 附件/视频 source | 代码块 | 备注 |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| AI 短剧 / AI 电影 Wiki | 133385 | 49 | 4 | 197 | 33 | 28 | 技能训练模板证据最强 |
| YouTube AI 视频 Wiki | 195002 | 181 | 4 | 38 | 49 | 24 | 运营课程闭环模板证据最强 |
| Claude Code 编程应用 Docx | 180341 | 219 | 0 | 638 | 0 | 87 | 项目实战入门模板证据最强 |
| Agent Skills PDF | 45 页 | 不适用 | 不适用 | 渲染页 | 不适用 | 不适用 | 文本层不可抽取，按视觉页分析 |

## 代表性图片样本

| 来源 | 原 token / src | 处理结果 | 本地文件 | 结构用途 |
| --- | --- | --- | --- | --- |
| Claude Code 教程 | `GACnbyeCpox6nwxs2f3chDMTnFe` | `media-download` 403，`media-preview` 成功 | `assets/feishu-samples/claude-code-01-project-overview.png` | 项目开头或路径图样本 |
| AI 短剧教程 | `YQGTbUhhyoW7zfxqjUEcZ9zcnfe` | `media-download` 403，`media-preview` 成功 | `assets/feishu-samples/ai-short-drama-01-five-stage-flow.webp` | 五阶段流程图样本 |
| YouTube AI 视频教程 | `MF1qbAWYKoJRtgx2IM7cVvUTnte` | `media-download` 403，`media-preview` 成功 | `assets/feishu-samples/youtube-ai-01-opening-evidence.webp` | 开头论证和案例证据样本 |

注意：`claude-code-01-project-overview.png` 的文件内容实际为 WebP，来自飞书预览接口返回的内容类型差异；保留原文件名用于复现 CLI 输出。

## PDF 渲染页

| 页码 | 本地文件 | 用途 |
| --- | --- | --- |
| 1 | `assets/pdf-pages/agent-skills-guide-page-01.png` | 封面定位、前置要求、指南承诺 |
| 2 | `assets/pdf-pages/agent-skills-guide-page-02.png` | 目录/开篇结构取样 |
| 3 | `assets/pdf-pages/agent-skills-guide-page-03.png` | 系统指南结构取样 |

## 资产使用结论

- 飞书教程的图片主要承担“真实界面证据、流程图、结果展示和视频位置指引”四类作用。
- 参考学习模式不应全量搬运图片，应先建立“图片在结构里承担什么教学功能”的资产卡。
- 如果目标是生成新教程，优先复用图片位置和功能，而不是复用原图。
- 如果目标是一比一复刻，必须另行确认复制、复刻或课堂使用权限。
