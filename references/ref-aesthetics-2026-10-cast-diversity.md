# 参考图提取补充 v2 · ref-2026-10-cast-diversity

来源：用户补充的 5 张图（走廊、储物柜区、教室）。补的是**非白人角色档、
真金发样本、以及可读身型与服装层次的中景**。

---

## 一、修一个过时的假设：`ethnicity` 不再默认白人

第一批 14 张里白人占多数，我当时把 `ethnicity` 的默认值写成了 `caucasian`。
**这批图证明那是错的**——这是一部**多族裔剧组**，而且这不是少数派特征，
是这部剧的常态。

| 观察 | 结论 |
| --- | --- |
| 白人、黑人、拉丁/地中海、混血同框 | 族裔是主要区分变量之一 |
| 深肤色角色出现在主角层（不只是点缀） | 不能当配角处理 |
| 同族裔内部的差异同样大（如两位深肤色角色的骨相完全不同） | 族裔不等于同一种脸 |

### 硬规则修正

- **`ethnicity` 不设默认值**。用户没指定时，按阵容需要主动分配多样性，
  **不允许整批默认成白人**。
- 一个剧组里至少应覆盖 **2 个以上族裔档**，除非用户明确要求单一族裔。
- **族裔不等于骨相**：指定族裔后，骨相仍要走 `face-diversity.md` 的差异下限，
  不能靠"肤色不同"当差异。

### 新增族裔档与配套参数

| `ethnicity` | 配套的骨相/皮肤倾向 |
| --- | --- |
| `black-african-american` | `deep-warm-luminous` 深暖有光泽的肤质；发 `tight-curl` / `coily-long` / `braided-long` / `natural-afro`；唇 `full`；鼻 `broad-flat` 或 `rounded-soft` 常见 |
| `black-mixed` | 肤色跨度大（`warm-light` 到 `deep-warm-tan`）；发常为 `curl-mixed` / `wavy-volume`；骨相自由 |
| `latina-mediterranean` | `olive-medium` 到 `deep-warm-tan`；发 `wavy-lob-highlighted` / `thick-wavy-long`；特征常在眉与眼 |
| `asian-east` | 发 `straight-sleek` / `straight-layered`；眼 `monolid` / `hooded` / `round-almond`；颧骨 `flat-to-subtle` |
| `caucasian` | 见青少年档原提取 |

**注意**：上表是**倾向**，不是规则。同族裔的角色之间必须按差异下限拉开——
两位深肤色女性的骨相可以一个是窄长脸+高鼻梁、一个是圆软脸+宽鼻头，
这正是本批图里实际存在的情况。

---

## 二、真金发样本（之前完全缺失）

青少年档里我写了"深色发为主，有少数提亮发的角色"，但没有金发样本。
这批图补上了，而且**真实的金发和"深发漂染"完全不同**：

```yaml
hair:
  color: pale-yellow-blonde          # 浅黄金，不是金色调
  tone: warm-not-ashy                # 暖金，不是冷灰金（关键区别）
  length: long
  volume: medium
  silhouette: straight-sleek          # 顺直
  layer_style: face-framing-layers    # 分层修饰脸型
  fringe: straight-full-bangs         # 直角齐刘海（不是空气刘海）
  texture: smooth
  root_darkening: none                # ★ 发根不发黑——这是真金发的标志
```

**判定要点**：`root_darkening: none`。漂染金发必然有深色发根，
提示词里如果不排除这一点，模型会给你一个"看起来像染的"金发。

**配套**：真金发通常伴随 `fair-warm` 肤色与浅色眼（蓝 / 灰蓝 / 灰绿），
且眉色**比发色深**（眉深发浅是金发的典型特征，不能统一成一色）。

---

## 三、中景带来的新信息：身型、手势、服装层次

之前全是胸像，这批教室与走廊镜头能看到肩线以下，补上了三块：

### 3.1 身型参数（新增维度）

批次观察：全员**偏瘦、肩线窄而干净**，没有健身型体格。

| 字段 | 本批次主力值 |
| --- | --- |
| build | `slim-teen` 偏瘦青春期体格 / `lean-athletic` 精瘦运动型 |
| shoulder_line | `narrow-clean` 肩窄且线条干净 |
| neck | `slender-defined` 颈部纤细、锁骨可见 |
| posture | `natural-slightly-relaxed` 自然略松、不是挺胸后仰 |

**注意与原始需求的冲突**：用户最初那段设定写的是"身材高挑修长、肩颈线条优越"——
**这批图证实了这个取向**，所以原始需求在这里是对的，可以保留为默认。

### 3.2 手势与身体语言（新增维度）

这批图的真实感有很大一部分来自**不完美的姿态**：

| 观察 | 可复用写法 |
| --- | --- |
| 抱着一叠文件、双臂交叠 | `arms-crossed-holding-papers` 双臂交叠抱文件 |
| 手插兜、身体重心偏一侧 | `hand-in-pocket-weight-shifted` 单手插兜重心偏一侧 |
| 坐在课桌前、一手拿笔一手按肚子 | 明确写出双手各自在做什么 |
| 说话时手部抬起比划 | `gesturing-mid-speech` |
| 转身回头、身体半侧 | `turned-half-profile` 半侧身回望 |

**规则**：中景以上**必须分别写清两只手在做什么**。
只写"双手自然垂落"在校园剧场景里是不真实的——学生手里总有东西。

### 3.3 服装层次（服装层终于可写了）

之前只有上衣颜色，现在能看到完整的层次结构：

```yaml
# 本批次常见的三层结构与单品
layering_patterns:
  - shirt-under-sweater          # 衬衫 + 针织衫（领口露出）
  - tee-under-open-button-up     # T恤 + 敞开穿的法兰绒/格子衬衫
  - crop-top-under-open-shirt    # 短上衣 + 敞开的格子衬衫
  - hoodie-alone                 # 卫衣单穿
  - quarter-zip-sweatshirt       # 半拉链运动衫
  - raglan-tee                   # 插肩袖T恤（撞色袖）

single_items:
  bottoms: [jeans-straight, jeans-skinny, cargo-pants, joggers, pleated-skirt]
  shoes: [sneakers-white, canvas-sneakers, ankle-boots]
  bags: [pink-backpack, canvas-tote, crossbody-bag]
  accessories: [baseball-cap, hoop-earrings, thin-chain-necklace, hair-tie-on-wrist]
  outerwear: [denim-jacket, varsity-jacket, open-flannel]
```

**palette 观察**：中性色（米白、浅灰、奶油）打底 + **单个亮色点缀**
（粉色背包、红色波点、蓝色背心、黄色文件夹）。这个规律值得写成规则：
**每套造型一个亮色，不要两个。**

---

## 四、影调修正：校园内景比先前判断的更暖

第一批我判断为"冷中性"，这批教室与走廊镜头显示**室内暖调更明显**：

| 项 | 修正后 |
| --- | --- |
| 室内色温 | **偏暖**（顶部荧光 + 窗光混合后仍偏暖黄） |
| 对比 | 低（暗部很浅，几乎是灰） |
| 饱和度 | 低，但比第一批估计的略高 |
| 背景 | 明显虚化，人群虚成色块 |
| 颗粒 | 细腻 |
| 高光 | 白色墙面与地板轻微过曝，不死白 |

**结论**：本剧的影调是**暖而低对比的写实**，不是冷调。
之前那条"阴影冷中性"应修正为"阴影浅灰略暖"。

---

## 五、对"输出类型"的提醒（新增规则）

这批图提醒了一件事：**不同景别要求的脸部信息量不同**。

| 输出类型 | 面部段落详细度 | 原因 |
| --- | --- | --- |
| 四格设定板 | 中等 | 脸只占画面约 1/4 |
| 单张特写肖像 | 最详细 | 脸部就是全部内容 |
| 中景/全身剧照 | **简略** | 注意力预算要腾给身型、手势、服装层次 |

**规则**：编提示词前先问输出类型。给中景图写满 8 行面部细节是浪费——
模型会把预算花在看不见的地方，反而让姿态和服装走形。

---

## 六、仍缺的样本

- 反派气质角色
- 情绪激烈状态（愤怒、崩溃、大哭）的面部
- 成年男性权威角色（成年档目前只有女性一张）
- 明确的**全身**镜头（当前中景到腰，裤型与鞋的细节仍不完整）
