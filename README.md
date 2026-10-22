# AI 美式短剧-人物三视图

这是一个用于生成欧美影视级角色设定图提示词的 Codex Skill。它把角色外观拆成结构化角色卡，再编译成可以直接复制到生图工具的中文或英文提示词，重点解决人物三视图、批量角色差异和同一角色多套造型的一致性问题。

## 适用场景

- 美式短剧、欧美电影、真人影视项目的人物设定
- 单个角色的正面、侧面、背面三视图
- 同一部剧的一组演员角色设定
- 同一角色的多套服装或场景造型
- 有参考照片或剧照，需要抽取脸型比例和整体影调

本 Skill 只生成提示词和角色卡，不直接调用生图平台，也不负责提交任务。

## 怎么使用

在 Codex 中加载本 Skill 后，直接描述你的角色需求。建议一次提供以下信息：

```text
请使用 us-tv-character-design Skill，设计一组美式短剧角色。

题材/年代/地域：现代都市 / 2020s / 纽约
角色：
1. Alex，男主，男性，28 岁，拉丁裔，律师
2. Maya，女主，女性，27 岁，黑人，记者
3. Owen，反派，男性，45 岁，白人，地产商
每个角色造型数：2
版式：四格人物设定板
输出：中文和英文双版
画幅：9:16
参考图：无
```

如果信息不完整，至少说明：角色数量、每个角色的戏剧功能、性别、年龄和族裔。题材、年代、地域、色调、画幅和造型数量可以不写，Skill 会采用默认值并声明推断。

## 默认输出

每个角色通常会得到：

1. 一段可直接复制的成品提示词；
2. 一张机器可读的角色卡（适合后续修改和复用）；
3. 一句批次一致性说明，解释角色之间的区分点。

默认使用 `character-board-4panel` 四格版式：左侧为面部高清头像，右侧为正面、侧面、背面全身三视图。也可以指定 `side-by-side` 双视图版式。

## 角色一致性规则

- 同一角色的多种造型会冻结骨相、五官、肤色、发色和身份特征。
- 同批角色至少在四项面部结构上形成差异，不能只换发色或衣服。
- 全批角色共用同一套影调、摄影、背景和画幅设置。
- 提示词默认包含无文字、无 logo、无水印等负面约束。
- 角色差异优先来自骨相、五官比例、发型、气质和配色，不靠随意添加皮肤瑕疵。

## 使用参考图

提供照片或剧照路径时，说明它是：

- **人物参考**：用于抽取脸长脸宽比、眼距、下颌角、鼻梁起点等可复用比例；
- **风格参考**：用于抽取色调、对比度、颗粒和光源性质。

Skill 会把参考图抽象成通用参数，不会直接输出具体名人姓名，也不会把参考照片简单改写成形容词描述。

## 相关文件

- [`SKILL.md`](SKILL.md)：完整工作流、硬性规则和交付规范
- [`references/character-card-template.md`](references/character-card-template.md)：角色卡字段模板
- [`references/element-pools.md`](references/element-pools.md)：面部、发型、衣橱等可选要素池
- [`references/prompt-architecture.md`](references/prompt-architecture.md)：提示词七层结构和负面词
- [`references/batch-and-consistency.md`](references/batch-and-consistency.md)：批量一致性检查
- [`references/reference-image-workflow.md`](references/reference-image-workflow.md)：参考图分析流程
- [`references/examples.md`](references/examples.md)：完整提示词示例

## 最小请求模板

```text
使用 us-tv-character-design。
角色：<姓名/代号>，<戏剧功能>，<性别>，<年龄>，<族裔>
题材：<题材>
时代与地域：<年代 / 地域>
造型数：<数量，默认 1>
版式：<character-board-4panel 或 side-by-side>
输出语言：<中文 / 英文 / 中英双版>
```

