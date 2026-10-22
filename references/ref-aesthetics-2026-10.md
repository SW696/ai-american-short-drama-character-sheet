# 参考图提取：ref-2026-10-us-teen-drama

来源：用户提供的 14 张欧美校园剧剧照（多场景、多角色、含成年配角）。
本文件记录**从这批图提取的参数与风格特征**，用于提升提示词精度。

> 提取的是**可通用的比例规律与影调特征**，不是复刻某张照片或某个真人。
> 具体人名不作为长相依据——参数才是。

---

## 一、最重要的发现：辨识度来源排序

这批图里各个角色差异极大，但它们**变的是同一组变量**。按贡献从高到低：

| 排名 | 变量 | 观察 |
| --- | --- | --- |
| 1 | **眉毛浓密度 + 眉色深浅** | 几乎全员浓眉、偏黑偏深。成年男性角色眉更粗且压眼 |
| 2 | **眼睛大小 + 眼白占比** | 偏大、偏圆润。眼型很少细长；眼白比例高，显得清亮 |
| 3 | **肤色深浅 + 冷暖** | 跨度极大（冷白 → 深橄榄 → 古铜），是最强区分变量 |
| 4 | 发色与发量 | 深色为主，发量厚。有少数提亮发的角色 |
| 5 | 唇形饱满度 | 女性偏饱满，男性中等；唇峰普遍不夸张 |
| 6 | 脸型 | **差异最小**的一维——全员中等偏长、轮廓柔和 |

**这条排序意味着**：想要做出这批图的观感，**应该先拉开"眉+眼+肤色"三项**，
而不是像常见做法那样先改脸型。脸型在这套美学里几乎是常量。

---

## 二、骨相与五官参数（提取值）

### 批次共性（所有角色共享的部分）

```yaml
face_shape: 中等偏长, 轮廓柔和        # 不是"修长椭圆"也不是"方正有棱"
jawline: soft-clean                 # 干净但**不锋利**（锋利的例子几乎没有）
cheekbones: flat-to-subtle          # 颧骨不突出，几乎看不到明显颧骨结构
brow_ridge: pronounced-to-heavy     # 男性的立体感主要来源
brow_density: thick                 # ★ 全员浓眉，这是本批次第一特征
brow_color: near-black-to-dark-brown
eye_size: large                     # ★ 眼睛偏大，不是"修长细眼"
eye_shape: round-almond             # 圆润杏仁，少细长
nose_tip: rounded-soft              # 鼻头圆润，很少"精致小巧"
```

### 男女分别的倾向

| 维度 | 女性倾向 | 男性倾向 |
| --- | --- | --- |
| `brow_shape` | 自然弧形偏平，不做精细修饰 | 平直、粗，轻压眼 |
| `lips` | `full-soft`（偏饱满柔润） | `medium`（中等，唇线清楚） |
| `eyes.gaze` | `direct-open` 或 `warm-friendly` | `quiet-observant` 或 `wary-guarded` |
| 面部立体感来源 | 颧骨与唇 | **眉骨与下颌前突**，不是下颌角 |
| 气质 | 明亮、直接、有活力 | 沉静、内敛、略带戒备 |

### 关键反例（有价值的少数派）

批次里有几张属于少数派，但它们**正是多样性来源**：

| 反例 | 特征 | 用途 |
| --- | --- | --- |
| 冷白皮 + 蓝灰眼 + 直黑长发的女性 | 高对比冷调，全批唯一 | 做"冷艳对照角色"的模板 |
| 深古铜皮 + 大风卷 + 浓眉的女性 | 暖深调，眉眼强度最高 | 做"热带/拉丁系角色"的模板 |
| 成熟中年男性（家长/权威角色） | 窄长脸、深眼窝、额纹 | 做家长、上司、导师类角色 |
| 浅金发 + 宽下颌 + 圆眼的男性 | 憨厚感，非精致型 | 做配角/挚友，避免全员主角脸 |

**保留少数派是刻意的**：如果整批角色都按主流特征做，立刻会模板化。

---

## 三、影调参数（写进 `styleLock` 的部分）

这是"同一部剧"观感的真正来源——比脸重要。

```yaml
# 影调
highlight_tint: 中性偏暖            # 外景高光带暖金；内景高光中性白
shadow_tint: 冷中性                 # 阴影偏冷但不发蓝，不是青绿调
contrast: medium-low               # 对比偏低，暗部保留细节，不死黑
saturation: low-medium             # 整体低饱和，肤色是画面里唯一的暖点
skin_saturation: 保留              # 肤色不像环境一样降饱和

# 质感
grain: fine-natural                # 细腻颗粒，不是纯数字干净
sharpness: moderate                # 不锐化。边缘柔和
skin_texture: retained             # ★ 保留毛孔、雀斑、肤质不均
skin_smoothing: none               # ★ 没有磨皮，这是本批次的硬特征

# 光学
depth_of_field: shallow            # 背景明显虚化
lens_feel: 50-85mm                 # 中长焦，透视压缩柔和
lighting_nature: soft-natural      # 柔光为主
lighting_source:
  interior: 侧窗自然光 + 顶部环境光
  exterior: 黄昏黄金时段暖光，或阴天柔光
rim_light: subtle-or-none          # 很少用硬轮廓光

# 构图
framing: medium-closeup-to-medium  # 胸像到半身为主
camera_height: eye-level           # 平视，不俯不仰

# 色彩锚点
palette_environment: 米白/浅灰/木色/深蓝   # 家居与校园的固有色
palette_wardrobe: 低饱和为主 + 单个亮色点缀   # 如红衣波点、蓝色背心
```

**特别提醒**：`skin_smoothing: none` 是这批图最值得保护的特征。
生图模型默认会磨皮，**必须在负面层显式反向约束**，否则整批观感会从"剧照"变成"网红图"。

---

## 四、对要素池的扩展

已登记进 `element-pools.md` 的 `ref-2026-10` 扩展池。主要新增：

- `face_shape`: `medium-long-soft`、`oval-round-soft`
- `brow_density`: `thick` 提为**本美学默认值**（原默认是 `thick-neat`，过整齐）
- `brow_shape`: `thick-straight-heavy`、`thick-natural-arched`
- `eye_size`: `large`、`very-large`（新增字段）
- `eye_white_ratio`: `high`（新增字段，决定"清亮感"）
- `eye_shape`: `round-almond`、`wide-almond`
- `skin.tone`: `warm-olive-medium`、`deep-warm-tan`、`cool-porcelain` 三档作为主力
- `nose_tip`: `rounded-soft` 提为主力
- `lips.fullness`: `full-soft`（女性默认）
- `hair.silhouette`: `long-straight-sleek`、`wavy-lob-highlighted`、`thick-textured-male`、`tight-curl-short`

---

## 五、使用方法

生成新角色时，按这个顺序取特征：

```
① 先定肤色档        ← 这是本批次最强的区分变量
② 再定眉浓密度与形状  ← 第二强
③ 再定眼睛大小与眼白比 ← 第三强
④ 最后才微调脸型      ← 差异最小，别在这里浪费注意力
⑤ 影调统一用第三节的 styleLock，不要逐角色改
```

**反向约束按 `skin.idealization` 分档（v5 修订）**：

```
clean-polished（默认档：校草 / 偶像 / 精英 / 主角）
  要保持：真实毛孔与皮肤质感，不得塑料磨皮
  要禁止：雀斑、痘印、痣、疤痕、色斑、眼镜压痕、眼袋、胡茬

natural-real / character-blemished（普通同学 / 配角 / 剧情需要的人物痕迹）
  不得把面部处理成理想化、无瑕疵、高度对称的完美脸
  不得磨皮或去除皮肤纹理
```

英文（clean-polished）：

```
keep visible skin texture and real pores, do not plastic-smooth or airbrush the skin;
clear even skin, no freckles, no acne marks, no mole, no scar, no under-eye bags or dark circles
```

> **v5 说明**：旧版把这四句当作"必带"，结果是**干净好看的选角也被强行加上雀斑与痘印**。
> 防磨皮（要质感）永远保留；制造缺陷（要瑕疵）只在人设需要时使用。

---

## 六、待补充

本批图偏重**青少年主角群**，以下类型样本不足，下次提供参考图时优先补：

- ~~中年女性权威角色~~ → **已补充**，见 [ref-aesthetics-2026-10-adult.md](ref-aesthetics-2026-10-adult.md)
- **中年男性**权威角色（成年样本目前只有女性一张）
- 反派型角色（如果能收到）
- 全身或半身的服装细节图（现有图以胸像为主，服装信息偏少）
- 不同光线条件下的同一角色（用于判断哪些特征稳定、哪些随光变）
- 情绪激烈状态下的面部（现有图多为平静或克制表情）
