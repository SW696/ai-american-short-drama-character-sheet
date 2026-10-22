# 完整样例

## 样例 0：原始需求 → 角色卡（拆解演示）

用户原始需求（中文长段落）经拆解后落成下列卡片。这是本 Skill 的**黄金样例**。

### `character-cards/char-lead-m-01.yaml`

```yaml
meta:
  id: char-lead-m-01
  name: ""
  role: lead
  gender: male
  age_range: 17-19
  source_note: 欧美青春片男主 + 高中棒球队队长 + 校园风云人物

archetype:
  primary: youthful-athlete-captain
  secondary: [campus-social-center]
  vibe_keywords: [少年感, 校园风云人物, 干净利落]

identity:
  ethnicity: caucasian
  face_shape: elongated-oval
  jawline: sharp-clean
  chin: slightly-pointed
  cheekbones: natural-subtle
  brow_ridge: pronounced
  eyes: {color: light-gray-blue, shape: elongated, gaze: quiet-restrained-thoughtful}
  brows: {density: thick-neat, shape: clearly-defined, color: dark-golden-brown}
  nose: {bridge: straight-high, tip: refined-small}
  lips: {fullness: thin-but-defined, cupids_bow: pronounced, corners: straight-natural}
  facial_hair: none
  skin:
    tone: cool-porcelain-translucent
    texture: realistic-pores-retained
    finish: subtle-natural-glow
    freckles_or_marks: none

hair:
  color: dark-golden-brown
  length: medium-short
  volume: dense
  silhouette: natural-airy
  layers: visible
  messiness: slight
  top: full
  fringe: natural-curled-falling
  sides_back: slightly-longer

wardrobe:
  category: sports-baseball
  palette: {primary: white, accent: blue}
  items:
    top: white-short-sleeve-baseball-jersey-with-blue-piping
    underlayer: blue-athletic-shirt
    bottom: white-baseball-pants
    belt: blue
    accessories: [white-sport-wristband]
    socks_shoes: white-baseball-socks-and-cleats
  fit: loose-clean
  detail: clear-contrast-trim

viewSpec:
  layout: side-by-side
  left: front-face-closeup
  right: front-full-body-standing
  left_focus: [light-colored-iris, dimensional-brows-eyes, straight-nose-bridge,
               clear-lip-shape, realistic-skin-detail]
  right_requirements: [full-head-to-sole, natural-standing-pose, arms-naturally-down,
                       eye-level-gaze]
  consistency_lock: [facial_features, hairstyle, skin_tone, wardrobe]

photo:
  background: seamless-pure-white
  lens: 85mm-portrait
  aperture: f/2.8-f/4
  lighting: studio-soft-even
  realism: photoreal-live-action
  text_in_image: none
  aspect_ratio: "9:16"

negative:
  [text, letters, watermark, logo, signature, extra_person, duplicate_face,
   face_mismatch_between_views, extra_fingers, deformed_hands, facial_hair,
   glasses, plastic_skin, over_smoothed, doll_like, heavy_makeup, cropped_feet]
```

**拆解映射**（原文片段 → 卡片字段）：

| 原文片段 | 落到 |
| --- | --- |
| 真人写实电影级人物设定图 | `photo.realism` + L1 |
| 纯白色无缝背景 | `photo.background` |
| 同一名年轻白人男性 / 完全一致 | `meta` + `viewSpec.consistency_lock` |
| 左侧正面近景特写 / 右侧全身站立 / 自然平视 / 无文字 | `viewSpec` + `photo.text_in_image` |
| 17–19 岁 / 高挑修长 / 锁骨清晰 | `age_range` + L3 身材句（不入卡，属编译层恒定句） |
| 冷白偏通透 / 真实纹理 / 细腻光泽 | `identity.skin` |
| 修长椭圆脸 / 下颌锋利 / 下巴微尖 / 颧骨自然 / 眉骨立体 | `identity` 骨相组 |
| 浅灰蓝 / 眼型修长 / 安静克制若有所思 | `identity.eyes` |
| 浓密整齐 / 眉形清晰 / 偏深金棕 | `identity.brows` |
| 高挺笔直 / 鼻头精致小巧 | `identity.nose` |
| 偏薄但清晰 / 唇峰明显 / 嘴角平直 / 无胡须 | `identity.lips` + `facial_hair` |
| 中短 / 浓密 / 蓬松 / 层次 / 微乱 / 顶部丰盈 / 前额自然卷刘海 / 两侧后侧略长 | `hair.*` |
| 白球衣 + 蓝滚边 + 蓝打底 + 白长裤 + 蓝腰带 + 白护腕 + 白球袜球鞋 | `wardrobe.*` |
| 85mm / 棚拍柔匀 / 高写实高细节 | `photo.*` + L6 |

**刻意丢弃的内容**：无。原文所有可目视验证的要求都已落字段。
原文若出现"气质再好一点""高级感"这类不可验证描述，则应丢弃——它们只会稀释权重。

原文中另有三句**不落卡、而落编译层恒定句**的内容，因为它们对同批所有角色都成立，
落卡会造成重复，也失去批次统一性：

| 原文片段 | 落点 |
| --- | --- |
| 身材高挑修长、肩颈线条优越、锁骨清晰 | 编译层恒定身材句（见 prompt-architecture L3 骨架） |
| 摄影棚柔和均匀布光 | `photo.lighting`（全批共享，写 styleLock） |
| 高写实、高细节、真实真人摄影质感 | `photo.realism`（全批共享，写 styleLock） |

---

### 编译产物 `prompts/char-lead-m-01.zh.txt`

```
真人写实电影级人物设定图，纯白色无缝背景，同一名年轻白人男性，左右人物的面部特征、
发型、肤色、服装完全一致。左侧为人物正面面部近距离特写，右侧为正面全身站立视图，
人物自然平视镜头，标准站姿，无文字。

约17—19岁，身材高挑修长，肩颈线条优越，锁骨清晰，整体气质带有浓郁欧美青春电影男主感，
兼具美国高中棒球队队长的少年感与校园风云人物气质；肤色冷白偏通透，保留真实自然皮肤纹理
和轻微细腻光泽，脸型偏修长的椭圆形，面部轮廓流畅清晰，下颌线锋利干净，下巴微尖，
颧骨自然，眉骨立体；五官高度精致，眼睛偏浅灰蓝色，眼型修长，眼神安静、克制、若有所思；
眉毛浓密整齐，眉形清晰，颜色为偏深的金棕色，与发色协调但仍保留一定存在感；
鼻梁高挺笔直，鼻头精致小巧，嘴唇偏薄但唇形清晰，唇峰明显，嘴角自然平直，无胡须。

中短长度，发量浓密，整体轮廓自然蓬松，带明显层次与轻微凌乱感，顶部丰盈，
前额垂落自然卷曲感刘海，两侧和后侧头发略长，发丝柔软，保留自然空气感。

身穿白色棒球比赛制服，上衣为白色短袖棒球球衣，版型宽松利落，边缘带清晰蓝色滚边细节，
内搭蓝色打底运动上衣；下身穿白色棒球长裤，搭配蓝色腰带，整体造型干净利落、
充满校园运动感；手腕佩戴白色运动护腕，脚穿适合棒球运动的白色球袜与运动鞋。

左侧特写重点表现浅色瞳孔、立体眉眼、挺直鼻梁、清晰唇形与真实皮肤细节；
右侧完整显示头顶至鞋底，双手自然垂落，摄影棚柔和均匀布光，85mm人像镜头，
f/2.8–f/4，高写实、高细节、真实真人摄影质感。

负面：画面中不得出现任何文字、字母、水印、签名、logo；不得出现第二个人；
左右两张脸必须是同一个人；不得裁切头顶与脚部；不得出现胡须、眼镜、塑料感磨皮皮肤；
手部不得畸形或多余手指。
```

---

## 样例 1：女主（演示 gender 切换的三处同步）

`character-cards/char-lead-f-01.yaml` 相对样例 0 的**差异**（其余字段不动）：

```yaml
meta:
  id: char-lead-f-01
  role: lead
  gender: female
  age_range: 17-19
  source_note: 美剧女主，冷艳精英气质，校园里的对手/暗恋对象

archetype:
  primary: cool-elegant
  secondary: [brittle-perfectionist]
  vibe_keywords: [冷艳, 克制, 有距离感]

identity:                       # ← 切换点 1：骨相与面部改用 §2 F 列
  ethnicity: caucasian
  face_shape: diamond
  jawline: delicate-defined
  chin: slightly-pointed
  cheekbones: high-elegant
  brow_ridge: moderate
  eyes: {color: green-gray, shape: almond, gaze: cold-observing}
  brows: {density: medium-natural, shape: arched, color: chestnut}
  nose: {bridge: delicate-straight, tip: upturned-subtle}
  lips: {fullness: medium, cupids_bow: pronounced, corners: slight-down}
  facial_hair: none
  skin:
    tone: fair-warm
    texture: youthful-fine
    finish: dewy
    makeup: clean-minimal

hair:                           # ← 切换点 2：发型改用 §4 F 列
  color: chestnut
  length: collarbone
  volume: medium
  silhouette: sleek-straight
  layers: face-framing
  messiness: none
  fringe: curtain-bangs
  styling: worn-down-natural
  sides_back: tucked-behind-ear

wardrobe:                       # ← 切换点 3：衣橱改用 §6 F 组合
  category: office-business-casual
  palette: {primary: camel, accent: charcoal}
  fit: tailored-fitted
  detail: minimal-seamless

negative:                       # 男性项出、女性项入
  [text, letters, watermark, logo, signature, extra_person, duplicate_face,
   face_mismatch_between_views, extra_fingers, deformed_hands, masculine_features,
   plastic_skin, over_smoothed, doll_like, cropped_feet]
```

**卡点**：只改了 `identity` 而没改 `hair` / `wardrobe`，会得到"女性脸 + 男性中短蓬松刘海 +
棒球服"——这正是 gender 切换最常见的失败形态。

---

## 样例 2：同一角色换造型（保持身份锚）

同一男主从"球场"到"校园日常"，**只允许改 `hair.styling` 与 `wardrobe`**：

```yaml
meta: {id: char-lead-m-01, ...}      # 身份锚原样复制，一字不改
hair:
  color: dark-golden-brown           # ← 发色不可变（属于身份锚的视觉延续）
  messiness: intentional-tousled     # ← 可改：造型层
  fringe: swept-side                 # ← 可改
wardrobe:
  category: highschool-casual        # ← 可改
  palette: {primary: navy, accent: cream}
  fit: oversized-relaxed
  detail: minimal-seamless
```

**约束**：发色、发长（长度档不变）、脸、肤、眉、眼全部锁定。
换色必须当新角色处理，否则同批会出现"同一张脸的不同发色"，观众会认成两个人。

---

## 样例 3：三联视图（可选版式）

需要更完整的转面参考时，把 `viewSpec` 换成：

```yaml
viewSpec:
  layout: triptych
  views: [front-face-closeup, side-profile, full-body-front]
  consistency_lock: [facial_features, hairstyle, skin_tone, wardrobe]
```

编译时 L2 改为：
`三栏并置人物设定图，纯白无缝背景，同一人物依次为正面面部特写、正侧面轮廓、正面全身，
三栏面部特征、发型、肤色、服装完全一致，无文字。`

三联更适合做**长期复用素材**（后续生成挂参考图），双联更适合**一次性交付**。
