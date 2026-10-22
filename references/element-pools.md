# 可枚举要素池

**规则**：角色卡里的值必须出自本表（或其显式扩展）。扩展新值时，先在此登记再使用。
中英对照给出，便于同时产出中文卡与英文提示词。

---

## 0. 性别切换（男女主可选）

切换 `gender` 时，以下三个分区必须**同时**切换，否则会生成性别错乱的混合体：

| 分区 | male 取用 | female 取用 |
| --- | --- | --- |
| 骨相与面部 | §2 M 列 | §2 F 列 |
| 发型 | §4 M 列 | §4 F 列 |
| 衣橱 | §6 M 列 | §6 F 列 |

共通免切换：§1 年龄、§3 皮肤、§5 摄影、§7 负面、§8 气质原型。

---

## 2a. 族裔档（★ 不设默认值）

**硬规则：`ethnicity` 不允许默认成 `caucasian`。**
用户没指定时，按阵容需要**主动分配多样性**；一个剧组至少覆盖 2 个族裔档，
除非用户明确要求单一族裔。依据见
[ref-aesthetics-2026-10-cast-diversity.md](ref-aesthetics-2026-10-cast-diversity.md)。

| `ethnicity` | 配套骨相 / 皮肤 / 发倾向（**倾向，不是规则**） |
| --- | --- |
| `black-african-american` | 肤 `deep-warm-luminous` 深暖有光泽；发 `tight-curl` / `coily-long` / `braided-long` / `natural-afro`；唇 `full`；鼻 `broad-flat` 或 `rounded-soft` |
| `black-mixed` | 肤色跨度大（`fair-warm` → `deep-warm-tan`）；发 `curl-mixed` / `wavy-volume`；骨相自由 |
| `latina-mediterranean` | 肤 `olive-medium` → `deep-warm-tan`；发 `wavy-lob-highlighted` / `thick-wavy-long`；特征常集中在眉与眼 |
| `asian-east` | 发 `straight-sleek` / `straight-layered`；眼 `monolid` / `hooded` / `round-almond`；颧骨 `flat-to-subtle` |
| `caucasian` | 见 §2b 扩展池 |

**关键提醒：族裔不等于骨相。** 指定族裔后，骨相仍必须走
[face-diversity.md](face-diversity.md) 的差异下限——**不能靠"肤色不同"当差异**。
两位深肤色角色的骨相可以一个是窄长脸+高鼻梁、一个是圆软脸+宽鼻头。

### 新增发色值（v2 补充）

| 值 | 说明 |
| --- | --- |
| `pale-yellow-blonde` | 浅黄金，**暖金不是冷灰金**；真金发的标志是 `root_darkening: none`（发根不发黑） |
| `coily-long` / `tight-curl` / `braided-long` / `natural-afro` | 深肤色角色常用 |

**金发配套规则**：真金发通常配 `fair-warm` 肤色与浅色眼，
且**眉色比发色深**——眉深发浅是金发的典型特征，**不能把眉发写成同一色**。

### 新增身型维度（v2 补充）

| 字段 | 本批次主力值 |
| --- | --- |
| build | `slim-teen` 偏瘦青春期体格 / `lean-athletic` 精瘦运动型 / `curvy-soft` 柔和有曲线 |
| shoulder_line | `narrow-clean` 肩窄线条干净 / `soft-sloped` 柔和溜肩 |
| neck | `slender-defined` 颈细锁骨可见 |
| posture | `natural-slightly-relaxed` 自然略松（**不是**挺胸后仰） |

**写作用法**：`build` / `shoulder_line` 对**中景与全身**有效，
四格版式与特写里几乎看不到，不必写。

---

## 1. 年龄档（共通）

| 值 | 含义 | 典型戏剧功能 |
| --- | --- | --- |
| `16-18` | 少年感未褪，面部线条仍柔 | 校园剧主角 |
| `17-19` | 大学新鲜人 / 高中高年级 | 青春片男主女主默认 |
| `20-24` | 大学生、初入职场 | 校园剧配角、都市剧新人 |
| `25-32` | 青年成熟 | 都市剧主角 |
| `33-42` | 成熟期 | 医疗/律政/罪案剧主角 |
| `43-58` | 中年 | 家长、上司、导师 |
| `59+` | 老年 | 家族长辈 |

### ★ 年龄档决定"皮肤参数档位"，不是只填个数字

**这是最容易出错的一处。** 年龄档一变，皮肤与骨相的取用方向**整体反转**：

| 维度 | 青少年档（`16-24`） | 成年权威档（`33+`） |
| --- | --- | --- |
| 皮肤纹理 | 毛孔保留、雀斑可见 | **表情纹可见**（额纹/眉间纹/法令纹/眼尾纹） |
| 轮廓饱满度 | 饱满 | **颧下轻微凹陷、面颊略塌** |
| 眼下 | 干净或天然卧蚕 | **轻度眼袋与泪沟** |
| 唇 | 饱满柔润 | **偏薄、唇线略模糊、唇周细纹** |
| 眉 | 浓密 | **中等偏细、外侧略稀疏** |
| 眼神 | 明亮直接 | **疲惫但专注** |
| 发 | 厚重有体积 | **发量略减、发际线可见、少量白发** |

**硬规则**：`age_range` 为 `33+` 时，**必须显式写年龄特征**，
并在负面层加 `不得去除皱纹`、`不得逆龄处理`。
不写的话模型会往年轻修——它的默认倾向就是"更好看"。

完整成年档参数与影调见 [ref-aesthetics-2026-10-adult.md](ref-aesthetics-2026-10-adult.md)。

**新增字段（成年档专用）**：

| 字段 | 可选值 |
| --- | --- |
| eye_details | `crows_feet_fine` 眼尾细纹 / `under_eye_hollowing` 眼下凹陷 / `slight_puffiness` 轻度眼袋 |
| skin.details | `forehead_lines` 额纹 / `glabellar_lines` 眉间纹 / `nasolabial_folds_faint` 轻微法令纹 / `perioral_lines` 唇周细纹 |
| hair.details | `visible_hairline` 发际线可见 / `light_graying` 少量白发 / `density_reduced` 发量略减 |
| gaze（成年档） | `tired-focused` 疲惫但专注 / `weary-authoritative` 疲惫但有权威感 |

---

## 2. 骨相与面部

### M（男性）
| 字段 | 可选值 |
| --- | --- |
| face_shape | `elongated-oval` 修长椭圆 / `square-angular` 方正有棱 / `rectangular` 长方 / `diamond` 菱形 / `round-soft` 圆润 / `round-broad` 圆而宽厚 / `long-narrow` 长而窄 / `triangle` 三角（下宽上窄） / `inverted-triangle` 倒三角（额宽颌窄） / `heart` 心形 |
| jawline | `sharp-clean` 锋利干净 / `defined-square` 方正明显 / `soft-rounded` 柔和 / `wide-heavy` 宽而厚重 / `narrow-tapered` 窄而收 / `asymmetric-slight` 轻微不对称 |
| chin | `slightly-pointed` 微尖 / `square` 方 / `rounded` 圆 / `cleft` 中间有缝 / `receding` 后缩 / `broad-flat` 宽平 |
| cheekbones | `natural-subtle` 自然 / `high-prominent` 高而突出 / `flat` 平 / `wide-set` 位置偏外 / `full-fleshy` 饱满有肉 |
| brow_ridge | `pronounced` 立体 / `moderate` 中等 / `soft` 柔和 / `heavy-overhang` 厚重压眼 |
| nose_bridge | `straight-high` 高挺笔直 / `roman` 鹰钩 / `broad-flat` 宽平 / `slightly-concave` 微凹 / `narrow-thin` 窄而薄 / `slightly-crooked` 轻微歪（旧伤感） / `short-flat` 短平 |
| nose_tip | `refined-small` 精致小巧 / `rounded` 圆 / `broad` 宽 / `bulbous` 肉厚 / `upturned-slight` 微翘 / `fleshy-wide` 宽厚有肉 |

### F（女性）
| 字段 | 可选值 |
| --- | --- |
| face_shape | `elongated-oval` 修长椭圆 / `heart` 心形 / `oval-soft` 柔椭圆 / `diamond` 菱形 / `square-angular` 方正有棱 / `round-youthful` 圆润少女感 / `round-full` 圆而饱满 / `long-narrow` 长而窄 / `wide-square` 宽方 |
| jawline | `delicate-defined` 精致清晰 / `soft-v-line` 柔和 V 线 / `angular` 有棱角 / `wide-strong` 宽而下颌明显 / `soft-double` 柔和略带肉感 / `asymmetric-slight` 轻微不对称 |
| chin | `slightly-pointed` 微尖 / `rounded` 圆 / `delicate-narrow` 小巧窄 / `square-slight` 略方 / `cleft` 中间有缝 / `receding-slight` 微后缩 |
| cheekbones | `natural-subtle` 自然 / `high-elegant` 高而优雅 / `full-soft` 饱满柔和 / `wide-set` 位置偏外 / `flat-low` 平而低 / `apple-round` 苹果肌明显 |
| brow_ridge | `moderate` 中等 / `pronounced` 立体 / `soft` 柔和 / `heavy-overhang` 厚重压眼 |
| nose_bridge | `straight-high` 高挺笔直 / `delicate-straight` 精致笔直 / `slightly-concave` 微凹 / `broad-flat` 宽平 / `narrow-thin` 窄而薄 / `slightly-crooked` 轻微歪 / `short-flat` 短平 / `aquiline-graceful` 微鹰钩而秀气 |
| nose_tip | `refined-small` 精致小巧 / `upturned-subtle` 微翘 / `rounded` 圆 / `bulbous` 肉厚 / `broad-flat` 宽平 / `fleshy-soft` 圆润有肉 |

### 辨识度维度（可选；★ 只用于"魅力点"，不用于"缺陷"）

**分工原则（v5 起）**：人物之间的区分靠**骨相与五官比例 + 发型 + 气质 + 配色**（见 §2 与
face-diversity 的差异下限）。本节的字段**不是必填**，也**不得**用来充当区分手段。

- **魅力点（aesthetic charm）**：`dimples` 酒窝 / `laugh-lines-young` 年轻笑纹 /
  `gap-teeth` 门牙缝——属于"好看的特征"，任何干净档都可用。
- **缺陷痕迹（blemish）**：`freckles-sparse` 雀斑 / `mole-cheek` 颊痣 / `brow-scar` 眉疤 /
  `eyebag-natural` 眼袋 / `under-eye-circles` 黑眼圈 / `birthmark-slight` 胎记 / 以及
  `skin_extra` 全部值——**仅在 `skin.idealization: character-blemished` 下使用**，
  且必须在卡里写明剧情或职业原因。`clean-polished` 档一律 `none`。

| 字段 | 可选值 |
| --- | --- |
| distinctive_features | `none`（默认）/ `dimples` 酒窝 / `gap-teeth` 门牙缝 / `laugh-lines-young` 年轻的笑纹 / ── 以下仅 character-blemished ── / `freckles-sparse` 稀疏雀斑 / `mole-cheek` 颊痣 / `crooked-tooth-slight` 轻微牙不齐 / `protruding-ears` 招风耳 / `brow-scar` 眉部旧疤 / `eyebag-natural` 天然卧蚕-眼袋 / `chipped-tooth` 缺角牙 / `birthmark-slight` 浅色胎记 / `under-eye-circles` 轻微黑眼圈 |
| asymmetry | `none`（默认）/ `slight-smile` 笑时嘴型轻微不对称（魅力向，可用）/ ── 以下仅 character-blemished ── / `slight-eyes` 双眼轻微不对称 / `slight-brow` 眉高轻微不同 / `slight-nose` 鼻梁轻微偏向 |
| skin_extra（仅 character-blemished） | `none`（默认）/ `stubble-shadow` 胡茬青影 / `razor-burn` 剃须泛红 / `acne-marks-slight` 轻微痘印 / `sun-burn-nose` 鼻梁晒红 / `chapped-lips` 唇部干裂 |
| casting_type | `leading-man` / `leading-woman` / `jock-athlete` / `girl-next-door` / `brain-nerd` / `goth-alt` / `cheer-captain` / `bad-boy` / `rich-preppy` / `outsider-weird` / `character-actor` / `hard-worker`（倾向表见 [face-diversity.md](face-diversity.md)） |

**使用要求**：两个字段都允许为 `none`。**不允许**为了"防模板化"而往脸上加缺陷——
防模板化靠差异下限（九项至少 4 项不同），不靠把脸弄脏。
`casting_type: character-actor` 的"任意特征"要求同样只在 `character-blemished` 档生效。

### 五官共通（眼 / 眉 / 唇）
| 字段 | 可选值 |
| --- | --- |
| eyes.color | `light-gray-blue` 浅灰蓝 / `deep-brown` 深棕 / `hazel` 浅褐绿 / `green-gray` 灰绿 / `dark-blue` 深蓝 / `amber` 琥珀 / `near-black` 近黑 / `pale-blue` 浅蓝 / `green-bright` 明亮绿 / `muddy-brown` 浑浊棕 / `heterochromia-slight` 轻微异色 |
| eyes.shape | `elongated` 修长 / `almond` 杏仁 / `round-open` 圆而睁 / `upturned-cat` 上挑 / `monolid` 单眼皮 / `deep-set` 深眼窝 / `hooded` 内双/眼皮覆盖 / `downturned-sad` 下垂（显忧郁） / `wide-set` 眼距偏宽 / `close-set` 眼距偏窄 / `small-narrow` 小而细 / `large-round` 大而圆 |
| eyes.gaze | `quiet-restrained-thoughtful` 安静克制若有所思 / `direct-confident` 直接自信 / `warm-friendly` 温暖友好 / `cold-observing` 冷峻审视 / `intense-driven` 强烈执着 / `wary-guarded` 戒备 / `tired-flat` 疲惫平淡 / `mischievous` 促狭顽皮 / `anxious-shifting` 不安游离 / `blank-dissociated` 空茫走神 / 【ref-2026-10】`direct-open` 直接明亮 / `quiet-observant` 安静观察 |
| brows.density | `thick-neat` 浓密整齐 / `medium-natural` 中等自然 / `sparse-light` 稀疏浅色 / `thick-unruly` 浓密杂乱 / `overplucked-thin` 过细（修饰过度） / `bushy-connected` 浓密近相连 |
| brows.shape | `clearly-defined` 眉形清晰 / `straight` 平直 / `arched` 弧形 / `angular-peak` 眉峰明显 / `flat-low` 平而低压眼 / `rounded-soft` 圆弧柔和 / `asymmetric-slight` 轻微不对称 |
| lips.fullness | `thin-but-defined` 薄但唇形清晰 / `medium` 中等 / `full` 饱满 / `very-full` 很饱满 / `thin-flat` 薄而平 / `wide-full` 宽而厚 / `small-pouty` 小而嘟 |
| lips.cupids_bow | `pronounced` 明显 / `subtle` 轻微 / `soft` 柔和 / `none-flat` 无明显唇峰 |
| lips.corners | `straight-natural` 自然平直 / `slight-up` 微上扬 / `slight-down` 微下垂 / `asymmetric-slight` 轻微不对称 |

---

## 3. 皮肤（共通，女性可加妆容项）

| 字段 | 可选值 |
| --- | --- |
| tone | `cool-porcelain-translucent` 冷白通透 / `fair-warm` 暖白 / `light-beige` 浅米 / `olive-medium` 橄榄中等 / `tan-golden` 古铜金 / `deep-brown` 深棕 / `rich-ebony` 深黑 |
| **idealization**★ | `clean-polished` 干净精修（**默认**：肤质均匀、无斑点无痕迹、无黑眼圈眼袋，毛孔级真实纹理保留）/ `natural-real` 自然写实（允许极淡肤色不均，不得当身份标识）/ `character-blemished` 人物痕迹（剧情需要才用：疤痕、痘印、疲惫痕迹） |
| texture | `realistic-pores-retained` 保留毛孔真实纹理 / `smooth-natural` 平滑自然 / `weathered` 有风化感 / `youthful-fine` 年轻细腻 |
| finish | `subtle-natural-glow` 轻微细腻光泽 / `matte-natural` 自然哑光 / `dewy` 水润 |
| freckles_or_marks | `none`（**clean-polished 档强制**）/ `light-freckles` 浅雀斑 / `beauty-mark` 痣点 / `scar-detail` 疤痕细节 —— 后三项仅 `natural-real` 极淡使用或 `character-blemished` |
| makeup（仅女性可选） | `bare-natural` 裸妆 / `clean-minimal` 干净极简 / `soft-everyday` 日常淡妆 / `defined-dramatic` 浓烈定义 |

**干净 ≠ 塑料**：`clean-polished` 档要在负面层保留 `plastic_skin` / `over_smoothed` /
`airbrushed` / `doll_like` / `waxy_skin`（防磨皮），同时**删掉**"不得理想化 / 不得去除瑕疵 /
必须保留雀斑痘印"这类会强行制造缺陷的反向约束，改为正面写明"肤色干净均匀、
无雀斑无痘印无痣无疤痕、无眼镜压痕无眼袋"。毛孔与皮肤质感照旧保留。

男性角色 `makeup` 字段不填，并在负面层加入 `heavy_makeup`。

---

## 2b. 扩展池 `ref-2026-10`（欧美校园剧选角美学）

来源与提取依据见 [ref-aesthetics-2026-10.md](ref-aesthetics-2026-10.md)。
**这一批是本 Skill 当前的主力档位**——它来自真实成品剧照的提取，比默认池更收敛。

**关键差异**：本美学下**脸型差异极小**，辨识度主要来自
`brow_density` + `eye_size` + `skin.tone` 三者的组合。取特征时优先拉开这三项。

| 字段 | 本美学主力值 |
| --- | --- |
| face_shape | `medium-long-soft` 中等偏长、轮廓柔和 / `oval-round-soft` 椭圆偏圆柔和 |
| jawline | `soft-clean` 干净但**不锋利**（默认；锋利下颌属少数派） |
| cheekbones | `flat-to-subtle` 颧骨不突出（默认） |
| brow_ridge | `pronounced` 立体 / `heavy-overhang` 厚重压眼（男性立体感主来源） |
| **brow_density** | `thick` 浓密（★ **全员默认**）/ `thick-heavy` 浓密厚重（成年男性） |
| **brow_color** | `near-black` / `dark-brown` / `dark-golden-brown` |
| brow_shape | `thick-straight-heavy` 浓密平直轻压眼 / `thick-natural-arched` 浓密自然弧形 |
| **eye_size**（新增字段） | `large` 大（**默认**）/ `very-large` 很大 / `medium` 中等 |
| **eye_white_ratio**（新增字段） | `high` 眼白占比高、显清亮（**默认**）/ `medium` |
| eye_shape | `round-almond` 圆润杏仁（**默认**）/ `wide-almond` 宽杏仁 / `large-round` 大而圆 |
| eyes.gaze（女性） | `direct-open` 直接明亮 / `warm-friendly` 温暖友好 |
| eyes.gaze（男性） | `quiet-observant` 安静观察 / `wary-guarded` 戒备 |
| nose_tip | `rounded-soft` 圆润柔和（**主力**）/ `refined-small` 精致小巧（少数派） |
| lips.fullness（女性） | `full-soft` 饱满柔润（**默认**）/ `medium` |
| lips.fullness（男性） | `medium` 中等、唇线清楚（**默认**） |
| lips.cupids_bow | `subtle` 轻微（**默认**，本美学唇峰不夸张） |
| skin.tone | `cool-porcelain-translucent` 冷白（少数派，用于高对比冷调角色）/ `fair-warm` 暖调浅 / `olive-medium` 橄榄中等（**主力**）/ `deep-warm-tan` 深暖古铜 |
| skin.texture | `realistic-pores-retained`（**必选**）/ `freckles-visible` 雀斑可见 |
| skin.finish | `matte-natural` 自然哑光（**默认**）/ `subtle-natural-glow` |
| hair.silhouette | `long-straight-sleek` 长直顺滑 / `wavy-lob-highlighted` 提亮波浪中长 / `thick-textured-male` 男性厚重有纹理 / `tight-curl-short` 短紧卷 / `wavy-shoulder-volume` 及肩大波浪 |

### 本美学的固定影调（写进 `styleLock`，全批不许改）

```
对比中低、暗部保留细节不死黑；整体低饱和，肤色是画面唯一暖点；
高光中性偏暖（外景更暖），阴影冷中性不发蓝；
细腻颗粒、不锐化、边缘柔和；浅景深；
柔光为主（内景侧窗自然光，外景黄昏暖光）；极少用硬轮廓光；
真人皮肤纹理完整保留，不磨皮。
```

### 本美学的反向约束（★ v5 起按 `skin.idealization` 分档，不再一律"不得理想化"）

任何使用本扩展池的提示词，**必须**在负面层携带防磨皮项（`plastic_skin` / `over_smoothed` /
`airbrushed` / `doll_like` / `waxy_skin`），**但"不得理想化 / 不得去除瑕疵"这两句只在
`natural-real` 与 `character-blemished` 档使用**：

```
clean-polished（默认，校草/偶像/精英/主角）：
  保持真实毛孔与皮肤质感，不得塑料磨皮；肤色干净均匀，
  不得出现雀斑、痘印、痣、疤痕、色斑、眼镜压痕、眼袋、胡茬。

natural-real / character-blemished：
  不得把面部处理成理想化、无瑕疵、高度对称的完美脸；
  不得磨皮或去除皮肤纹理。
```

原因：生图模型默认会磨皮并向"标准好看"收敛，所以防磨皮项必须留；
但反过来强制"不得理想化"会**逼模型往脸上加瑕疵**——干净好看的选角会因此变脏脸。
两者的区别是"要皮肤质感"还是"要皮肤缺陷"：前者永远要，后者只在人设需要时才有。

### 本美学的少数派角色（刻意保留，作为多样性来源）

| 少数派 | 特征 | 用来做什么角色 |
| --- | --- | --- |
| 冷调高对比女性 | 冷白 + 蓝灰眼 + 长直黑发 | 冷艳对照角色 |
| 暖深调女性 | 深古铜 + 大风卷 + 浓眉 | 热带/拉丁系角色 |
| 中年权威男性 | 窄长脸 + 深眼窝 + 额纹 | 家长/上司/导师 |
| 憨厚非精致男性 | 浅金发 + 宽下颌 + 圆眼 | 配角/挚友（避免全员主角脸） |

---

## 4. 发型

### M（男性）
| 字段 | 可选值 |
| --- | --- |
| color | `dark-golden-brown` 深金棕 / `jet-black` 乌黑 / `dark-brown` 深棕 / `ash-blond` 灰金 / `warm-blond` 暖金 / `auburn` 赤褐 / `silver-gray` 银灰 |
| length | `short-cropped` 短发 / `medium-short` 中短 / `medium` 中长 / `shoulder` 及肩 |
| volume | `dense` 浓密 / `medium` 中等 / `fine` 细软 |
| silhouette | `natural-airy` 自然蓬松空气感 / `sleek-flat` 服帖 / `voluminous-quiff` 蓬起 / `tousled` 凌乱 |
| layers | `visible` 层次明显 / `blunt` 齐整 / `graduated` 渐层 |
| messiness | `slight` 轻微 / `none` 无 / `intentional-tousled` 刻意凌乱 |
| top | `full` 丰盈 / `flat-natural` 自然平 |
| fringe | `natural-curled-falling` 前额垂落自然卷曲 / `swept-side` 侧分 / `straight-forward` 前梳 / `none-exposed-forehead` 无刘海露出额头 |
| sides_back | `slightly-longer` 略长 / `tapered-clean` 收干净 / `short-fade` 短渐变 |

### F（女性）
| 字段 | 可选值 |
| --- | --- |
| color | 同 M 池，另加 `platinum-blonde` 铂金 / `copper-red` 铜红 / `chestnut` 栗棕 |
| length | `short-bob` 短波波 / `chin-length` 及颌 / `collarbone` 及锁骨 / `mid-back` 及背中 / `long` 长发 |
| volume | 同 M |
| silhouette | `natural-airy` / `sleek-straight` 顺直服帖 / `soft-waves` 柔和波浪 / `tousled` |
| layers | `visible` / `blunt` / `graduated` / `face-framing` 修饰脸型 |
| messiness | `slight` / `none` / `windblown-natural` 自然风吹感 |
| fringe | `natural-curled-falling` / `curtain-bangs` 中分八字 / `blunt-bangs` 齐刘海 / `swept-side` / `none-exposed-forehead` |
| styling | `worn-down-natural` 自然披散 / `half-up` 半扎 / `low-ponytail` 低马尾 / `high-ponytail` 高马尾 / `loose-braid` 松辫 / `messy-bun` 随性丸子头 |
| sides_back | `slightly-longer` / `tucked-behind-ear` 别到耳后 / `tapered-clean` |

---

## 5. 摄影与视图（共通）

| 字段 | 可选值 |
| --- | --- |
| background | `seamless-pure-white` 纯白无缝 / `seamless-light-gray` 浅灰无缝 / `studio-gradient` 影棚渐变 / `environmental` 实景（须另给场景描述） |
| lens | `85mm-portrait` / `50mm-natural` / `135mm-compressed` 长焦压缩 |
| aperture | `f/2.0` / `f/2.8-f/4` / `f/5.6` |
| lighting | `studio-soft-even` 柔和均匀 / `rembrandt-dramatic` 伦勃朗戏剧光 / `high-key-bright` 高调明亮 / `low-key-moody` 低调沉郁 |
| layout | `side-by-side` 左右并置（左特写+右全身） / `character-board-4panel` **四格设定板**（见下方专节，推荐） / `single-view` 单视图 / `triptych` 三联（正/侧/背） |

### 版式专节：`character-board-4panel` 四格设定板（推荐）

左侧高清正面头像 + 右侧正面/侧面/背面全身三视图。**核心机制：右侧正面与侧面全身图故意
糊脸**，于是"三个视图的脸是不是同一个人"这个问题不再存在——一致性压力被消掉。
左侧头像成为整张图唯一的身份裁决依据。

四格编译时必须包含的四条（缺一条版式就崩）：

1. 左侧头像：`面部为整张图唯一的身份裁决依据，必须清晰锐利、高细节`
2. 右侧正面与侧面全身图：`面部做柔和景深模糊处理，五官细节不可辨`
3. 背面全身图：`保留完整头部与发型`（必须写例外，否则背面也会被糊掉）
4. 负面层加：`比例尺`、`标签`、`视图名`、`网格线`、`重复视图`

四格版式下，**发型与发色是唯一的身份线索**（脸糊了），因此 `hair` 字段的一致性优先级
高于双视图版式，背面视图要显式描述后发长度与发尾形状。
| aspect_ratio | `9:16` 竖 / `3:4` 竖 / `16:9` 横 / `1:1` 方 |

---

## 5b. 镜头内身体语言（仅中景 / 全身需要）

**硬规则：中景以上的镜头必须分别写清两只手在做什么。**
只写"双手自然垂落"在校园剧场景里不真实——学生手里总有东西。

依据见 [ref-aesthetics-2026-10-cast-diversity.md](ref-aesthetics-2026-10-cast-diversity.md)。

| 字段 | 可选值 |
| --- | --- |
| gesture | `arms-crossed-holding-papers` 双臂交叠抱文件 / `hand-in-pocket-weight-shifted` 单手插兜重心偏一侧 / `one-hand-bag-strap` 单手扶包带 / `both-hands-phone` 双手持手机 / `gesturing-mid-speech` 说话时抬手比划 / `holding-notebook-and-pen` 一手持本一手握笔 / `hand-on-backpack-strap` 手抓背包带 / `arms-crossed` 单纯抱臂 |
| body_orientation | `frontal` 正面 / `turned-half-profile` 半侧身 / `turned-half-profile-glancing-back` 半侧回望 / `three-quarter` 四分之三侧 |
| framing | `closeup-face` 面部特写 / `medium-closeup` 胸像 / `medium` 半身 / `medium-full` 大半身 / `full-body` 全身 |

**详细度规则（重要，避免浪费提示词预算）**：

| 输出类型 | 面部段落 | 身体语言 |
| --- | --- | --- |
| 四格设定板 | 中等 | 不需要（版式固定站姿） |
| 单张特写肖像 | **最详细** | 不需要 |
| 中景 / 全身剧照 | **简略** | **最详细**（姿势、双手、服装层次） |

给中景图写满八行面部细节是浪费——模型会把预算花在看不见的地方，
反而让姿态和服装走形。

---

## 5c. 服装层次结构（v2 补充）

之前只有上衣颜色，现在补上完整的层次与单品池：

| 字段 | 可选值 |
| --- | --- |
| layering_pattern | `shirt-under-sweater` 衬衫+针织衫（领口露出）/ `tee-under-open-button-up` T恤+敞开格纹衬衫 / `crop-under-open-shirt` 短上衣+敞开衬衫 / `hoodie-alone` 卫衣单穿 / `quarter-zip-sweatshirt` 半拉链运动衫 / `raglan-tee` 插肩撞色袖T恤 / `tank-alone` 背心单穿 |
| bottoms | `jeans-straight` / `jeans-skinny` / `cargo-pants` / `joggers` / `pleated-skirt` |
| shoes | `sneakers-white` / `canvas-sneakers` / `ankle-boots` |
| bags | `backpack` / `canvas-tote` / `crossbody-bag` |
| accessories | `baseball-cap` / `hoop-earrings` / `thin-chain-necklace` / `hair-tie-on-wrist` |
| outerwear | `denim-jacket` / `varsity-jacket` / `open-flannel` |

**配色规则（v2 新增）**：中性色（米白 / 浅灰 / 奶油 / 牛仔蓝）打底，
**每套造型只加一个亮色点缀**（粉色背包、红色波点、蓝色背心、黄色文件夹）。
两个亮色就会从"剧照"变成"杂志大片"。

---

## 6. 衣橱体系（一主色 + 一辅色，禁止多色堆叠）

结构固定为：`category（场景职业）` × `palette（主色+辅色）` × `fit（版型）` × `detail（细节）`。

| category 值 | 场景 |
| --- | --- |
| `sports-baseball` | 棒球训练/比赛 |
| `sports-generic` | 通用运动 |
| `school-uniform` | 私立学校制服 |
| `highschool-casual` | 高中日常休闲 |
| `college-casual` | 大学休闲 |
| `cheer-squad` | 啦啦队 |
| `street-urban` | 街头潮流 |
| `office-formal` | 正装职场 |
| `office-business-casual` | 商务休闲 |
| `medical-scrubs` | 医疗 |
| `police-detective` | 警探 |
| `evening-formal` | 晚宴礼服 |

| 字段 | 可选值 |
| --- | --- |
| palette.primary | `white` / `black` / `navy` / `charcoal` / `beige` / `cream` / `olive` / `camel` / `burgundy` / `forest-green` |
| palette.accent | 同上（应与 primary 有明度对比） |
| fit | `loose-clean` 宽松利落 / `tailored-fitted` 修身 / `oversized-relaxed` 廓形慵懒 / `athletic-compression` 运动贴合 |
| detail | `clear-contrast-trim` 清晰撞色滚边 / `minimal-seamless` 极简无装饰 / `visible-stitching` 明线 / `subtle-texture` 面料纹理 |

**M 常见组合**
- `sports-baseball` + white/blue + loose-clean + 撞色滚边
- `highschool-casual` + navy/cream + oversized-relaxed + 极简
- `street-urban` + black/olive + oversized-relaxed + 明线

**F 常见组合**
- `cheer-squad` + white/burgundy + athletic-compression + 撞色
- `school-uniform` + navy/cream + tailored-fitted + 极简
- `college-casual` + cream/olive + oversized-relaxed + 面料纹理
- `office-business-casual` + camel/charcoal + tailored-fitted + 极简

---

## 7. 负面约束池（按角色挑选，基础集必带）

| 基础集（必带） | `text`, `letters`, `watermark`, `logo`, `signature`, `extra_person`, `duplicate_face`, `face_mismatch_between_views` |
| --- | --- |
| 手部集 | `extra_fingers`, `deformed_hands`, `extra_limbs`, `mutated_hands` |
| 真实感集 | `plastic_skin`, `over_smoothed`, `doll_like`, `cgi_look`, `airbrushed`, `waxy_skin` |
| 男性加带 | `facial_hair`, `heavy_makeup`, `feminine_features` |
| 女性加带 | `masculine_features`, `heavy_masculine_jaw` |
| 版式集 | `split_screen_lines`, `frame_border`, `cropped_feet`, `cropped_head`, `collage` |

---

## 8. 气质原型（决定其余一切选择；同批相邻角色须错开）

| 值 | 中文 | 常配骨相 | 常配衣橱 | 常配眼神 |
| --- | --- | --- | --- | --- |
| `youthful-athlete-captain` | 阳光运动队长 | `elongated-oval` / `square-angular` | `sports-baseball`, `sports-generic` | `direct-confident` |
| `quiet-intellectual` | 安静学霸 | `elongated-oval` | `school-uniform`, `college-casual` | `quiet-restrained-thoughtful` |
| `moody-artistic` | 忧郁文艺 | `diamond` | `street-urban`, `highschool-casual` | `cold-observing` |
| `campus-social-center` | 校园风云人物 | `square-angular` | `highschool-casual`, `street-urban` | `warm-friendly` |
| `driven-striver` | 目标导向的奋斗者 | `rectangular` | `office-business-casual` | `intense-driven` |
| `warm-girl-next-door` | 邻家温暖女孩 | `oval-soft` / `heart` | `college-casual` | `warm-friendly` |
| `cool-elegant` | 冷艳精英 | `diamond` / `elongated-oval` | `office-formal` | `cold-observing` |
| `rebel-outsider` | 叛逆局外人 | `square-angular` / `diamond` | `street-urban` | `wary-guarded` |
| `sunshine-cheerleader` | 阳光活力女 | `round-youthful` / `heart` | `cheer-squad` | `direct-confident` |
| `brittle-perfectionist` | 脆弱完美主义 | `heart` / `elongated-oval` | `office-formal`, `school-uniform` | `quiet-restrained-thoughtful` |

**配对建议**：男主 + 女主的组合优先取"互补而非同类"，例如
`youthful-athlete-captain` × `cool-elegant`、`quiet-intellectual` × `sunshine-cheerleader`。
同类组合会让双人同框图缺乏张力，也更容易在批量里混淆两人身份。

---

## 9. 扩展池 `sports-motorsport`（v4，2026-10 赛车/赛道题材）

**登记原因**：用户需求"白色赛车服 + 白色头盔"在 §6 衣橱体系里没有对应 category，
按池规则先登记再使用。本区块为**追加**，不改动任何既有值。

### 9a. 新增 category

| 值 | 场景 |
| --- | --- |
| `sports-motorsport` | 方程式/房车/卡丁车赛道、车队制服、颁奖台 |

### 9b. 新增单品值（供 `wardrobe.items` 使用）

| 字段 | 可选值 |
| --- | --- |
| suit | `one-piece-racing-suit` 连体赛车服 / `racing-jacket-and-pants` 上衣+长裤分体 |
| underlayer | `fireproof-undershirt-collar-clean` 阻燃内衣领口收净 |
| headgear | `full-face-racing-helmet-carried` 全罩盔**手持/环抱**（不遮挡面部与发型）/ `full-face-racing-helmet-worn-visor-closed` 全罩盔**佩戴、面镜闭合** / `open-face-helmet-carried` 半盔手持 |
| gloves | `racing-gloves` 赛车手套 |
| footwear | `racing-boots` 赛车靴 |
| harness | `six-point-harness-over-suit` 六点式安全带（仅座舱内景，设定图不用） |

### 9c. 新增配件值（§5c accessories 追加）

`racing-helmet-carried` / `racing-helmet-worn` / `racing-gloves` / `hans-device` /
`team-radio-earpiece` / `balaclava-under-helmet`

### 9d. 新增负面值（§7 追加）

| 值 | 用途 |
| --- | --- |
| `sponsor_logos` | 赛车服/头盔上的赞助商标志 |
| `brand_marks_on_garment` | 服装商标 |
| `numbers_on_garment` | 车号/编号贴纸 |
| `cropped_helmet` | 头盔被裁切 |
| `helmet_covering_face` | 头盔遮住面部或发型（手持盔版必带） |
| `helmet_on_in_closeup` | 左侧特写戴盔（手持盔版必带） |

### 9e. 本题材的两条使用提醒

1. **头盔是"身份线索杀手"**：`character-board-4panel` 依赖发型发色作为糊脸视图的唯一身份线索，
   头盔一戴这条线索就断了。默认做法是**手持/环抱头盔**（`...-carried`），
   把头盔当作道具而不是头饰；确实要出戴盔造型时，按"新造型"处理（同卡新增 wardrobe 变体，
   `identity` 与 `hair` 逐字不变），并让左侧特写保持不戴盔。
2. **赛车服天生带满赞助商文字**：该题材的负面层必须显式携带
   `sponsor_logos` / `brand_marks_on_garment` / `numbers_on_garment`，
   否则成图上会出现乱码字母与假商标。这一条与 §7 基础集的 `text` / `logo` 不重复，
   因为基础集压不住"服装贴片"这类结构化元素。

### 9f. 新增负面值（§7 追加，ref-2026-10 两条反向约束的机械写法）

| 值 | 用途 |
| --- | --- |
| `idealize_face` | 不得把面部处理成理想化、无瑕疵的完美脸 |
| `perfect_symmetry` | 不得做成高度对称的脸 |
| `remove_skin_texture` | 不得磨皮或去除皮肤纹理 |

**说明**：ref-aesthetics-2026-10.md 第五节要求的这两句反向约束，此前只能写成中文句子；
登记为枚举值后，角色卡与提示词可以用同一批 token 表达，便于批量查重与自动校验。
