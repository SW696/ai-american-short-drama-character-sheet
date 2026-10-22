# 角色卡模板与填写口径

角色卡是**唯一事实来源**：提示词由它编译、一致性由它校验、批量由它驱动。
填写顺序即字段顺序，不要打乱。

## 目录结构

```yaml
meta:        # 身份与管理信息
archetype:   # 戏剧气质（决定其余一切选择）
identity:    # ★ 身份锚：冻结后逐字复用
hair:        # 造型锚：稳定，但可换造型
wardrobe:    # 造型层：最易变
viewSpec:    # 视图契约
photo:       # 摄影技术参数
negative:    # 负面约束
```

---

## 完整模板（含注释）

```yaml
meta:
  id: char-lead-m-01            # 稳定业务键，全流程引用它，不用中文名
  name: ""                      # 剧中人名，可空
  role: lead                    # lead | co-lead | supporting | antagonist | mentor
  gender: male                  # male | female | unspecified
  age_range: 17-19
  source_note: ""               # 用户原话要点，便于回溯

archetype:
  primary: youthful-athlete-captain     # 见 element-pools「气质原型」
  secondary:                            
    - campus-social-center
  vibe_keywords:                # 3-5 个中文气质词，供中文卡与选片参考
    - 少年感
    - 干净利落
    - 校园风云人物

identity:                       # ★ 身份锚：同角色所有图逐字复用，禁止改写
  ethnicity: caucasian          # ★ 不设默认！按阵容主动分配，见 element-pools §2a
  casting_type: leading-man            # ★ 决定面部特征取用倾向，见 face-diversity.md
  face_shape: elongated-oval           # 修长椭圆形
  jawline: sharp-clean                 # 下颌线锋利干净
  chin: slightly-pointed               # 下巴微尖
  cheekbones: natural-subtle           # 颧骨自然
  brow_ridge: pronounced               # 眉骨立体
  eyes:
    color: light-gray-blue             # 浅灰蓝色
    shape: elongated                   # 眼型修长
    gaze: quiet-restrained-thoughtful  # 安静克制若有所思
  brows:
    density: thick-neat
    shape: clearly-defined
    color: dark-golden-brown           # 偏深金棕，与发色协调
  nose:
    bridge: straight-high
    tip: refined-small
  lips:
    fullness: thin-but-defined
    cupids_bow: pronounced             # 唇峰明显
    corners: straight-natural          # 嘴角自然平直
  distinctive_features: none            # 可选，默认 none。★ 只填"魅力点"：dimples / laugh-lines-young / gap-teeth
  asymmetry: none                       # 可选，默认 none。slight-smile 属魅力向可用；其余不对称仅 character-blemished 档
  facial_hair: none                    # ★ 男性默认 none；女性恒为 none
  skin:
    idealization: clean-polished       # ★ 必填。clean-polished（默认，干净精修）/ natural-real / character-blemished
    tone: cool-porcelain-translucent   # 冷白偏通透
    texture: realistic-pores-retained  # 保留真实自然皮肤纹理（防塑料感，与干净度无关）
    finish: subtle-natural-glow        # 轻微细腻光泽
    freckles_or_marks: none            # clean-polished 档恒为 none
    skin_extra: none                   # 仅 character-blemished 档可用：stubble-shadow / razor-burn / acne-marks-slight

hair:
  color: dark-golden-brown
  length: medium-short
  volume: dense
  silhouette: natural-airy            # 自然蓬松、保留空气感
  layers: visible
  messiness: slight
  top: full
  fringe: natural-curled-falling      # 前额垂落自然卷曲感刘海
  sides_back: slightly-longer
  styling: worn-down-natural          # 女性角色常用：披散/半扎/马尾等
  note_for_female: ""                 # 记录女性角色的长度/束发差异

wardrobe:
  category: sports-baseball           # 见 element-pools「衣橱体系」
  palette:
    primary: white
    accent: blue
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
  - text
  - letters
  - watermark
  - logo
  - signature
  - extra_person
  - duplicate_face
  - extra_fingers
  - deformed_hands
  - facial_hair              # 按需：无胡须角色必带
  - glasses
  - plastic_skin
  - over_smoothed
  - heavy_makeup             # 男性角色建议带
  - face_mismatch_between_views
```

---

## 填写口径（易错项）

- **枚举必须来自 element-pools**。想表达池子里没有的特质：先扩池，再加进卡。
  临时造词会导致同一批里语义漂移。
- **`identity` 不写程度副词**。"非常锋利"没用；`sharp-clean` 才是可复用值。
- **一个字段只表达一件事**。`jawline: sharp-clean-and-masculine` 是错的：
  `masculine` 属于 `archetype`。
- **`hair` 与 `identity` 分离**：允许角色换发型但保留人脸；若剧情要求"换发色"，
  那是**新造型**，必须新建 `wardrobe` + `hair` 组合，不得覆盖原卡。
- **`facial_hair` 对女性角色必须为 `none`**；对男性角色按人设填，未指定填 `none`
  并同步写入负面层。
- **`viewSpec.consistency_lock` 不可删减**，四项就是这类设定图的成败点。
- **`meta.id` 稳定不变**。改名可以，改 id 会断掉已生成的锚点关联。

---

## 校验（编译提示词前自查）

1. 所有枚举值都能在 element-pools 找到出处
2. `identity` 无空字段
3. `consistency_lock` 四项齐全
4. `negative` 非空且含 `text` / `watermark` / `extra_person`
5. `photo.background` 与 `viewSpec` 不矛盾
6. 同批角色之间：`identity` 九项中**至少 4 项不同**（外加 `eyes.color`、`hair.color` 必查）
7. `skin.idealization` 已声明；**除 `character-blemished` 档外，正面描述里不得出现
   雀斑 / 痘印 / 痣 / 疤痕 / 色斑 / 眼镜压痕 / 眼袋 / 黑眼圈 / 胡茬**（负面层里"不得出现…"不算）
8. 对照片 face-diversity.md 的「模板脸自检」五问，无一命中
