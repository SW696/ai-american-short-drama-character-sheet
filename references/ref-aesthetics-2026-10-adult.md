# 参考图提取补充 · ref-2026-10-adult

来源：用户提供的成年女性权威角色剧照（办公场景，打电话，职业装）。
补的是 `ref-aesthetics-2026-10.md` 里标注的空缺项。

---

## 一、这张图带来的新维度：年龄特征

前 14 张全是青少年——**皮肤无纹、轮廓饱满、无下垂**。
这张完全不同，它证明了本批次美学里**还存在一个"成年权威"档位**，
而它的皮肤参数与青少年档**方向相反**。

这是之前完全没覆盖的一层。如果不单独建这个档位，
生成成年角色时会套用青少年参数，得到"没有年龄感的成年人"——一眼假。

| 维度 | 青少年档（ref-2026-10） | 成年权威档（本档） |
| --- | --- | --- |
| 皮肤纹理 | 毛孔保留、雀斑可见 | **表情纹可见**（额纹、眉间纹、法令纹、眼尾纹） |
| 轮廓饱满度 | 饱满 | **面颊轻微塌陷、颧下凹陷** |
| 眼下 | 干净或天然卧蚕 | **轻度眼袋与泪沟** |
| 唇部 | 饱满柔润 | **偏薄、唇线略模糊、唇周细纹** |
| 眉 | 浓密 | **中等偏细、外侧略稀疏** |
| 眼神 | 明亮直接 | **疲惫但专注** |
| 发 | 厚重有体积 | **发量略减、发际线可见、有白发** |

**硬规则**：成年角色**必须**显式写年龄特征。不写的话模型会往年轻修，
因为它的默认倾向就是"更好看"。

---

## 二、本档提取值

```yaml
# 骨相
face_shape: medium-length-oval-oblique    # 中等长度、椭圆偏方
jawline: soft-defined-slight-jowl         # 柔和有轮廓，下颌轻微松弛
cheekbones: subtle-with-hollowing         # 颧骨可见 + 颧下轻微凹陷
brow_ridge: subtle                        # 眉骨不突出（与青少男档的 pronounced 相反）

# 眉眼
eye_size: medium                          # 中等（青少年档是 large）
eye_shape: hooded                         # 眼皮覆盖，随年龄加深
eye_color: dark-blue-gray                 # 深蓝灰
eye_details:                              # ★ 新增字段：眼部年龄细节
  - crows_feet_fine                       # 眼尾细纹
  - under_eye_hollowing                   # 眼下轻微凹陷
  - slight_puffiness                      # 轻度眼袋
gaze: tired-focused                       # ★ 疲惫但专注（新增值）
brow_expression: slight_frown             # 轻微蹙眉（情绪特征，可保留）
brow_density: medium-thin                 # 中等偏细
brow_outer_thinning: true                 # ★ 眉头外侧稀疏

# 鼻唇
nose_bridge: straight-with-soft-tip
nose_tip: rounded-soft
lips.fullness: thin-to-medium             # 偏薄
lips.cupids_bow: subtle                   # 唇峰不明显
lips.corners: slight-down                 # 嘴角微下垂
perioral_lines: faint                     # ★ 唇周细纹

# 皮肤（本档核心）
skin.tone: fair-cool-neutral              # 冷中性白
skin.texture: mature-visible-lines        # ★ 表情纹可见
skin.details:                             # ★ 新增字段
  - forehead_lines                        # 额纹
  - glabellar_lines                       # 眉间纹
  - nasolabial_folds_faint                # 轻微法令纹
skin.finish: matte-natural                # 哑光，无光泽
skin.makeup: clean-minimal                # 干净淡妆，不遮皱纹（重要）
facial_hair: none

# 发
hair.color: medium-brown
hair.length: shoulder-length
hair.volume: medium-reduced               # 发量略减
hair.silhouette: smooth-slightly-flat     # 顺滑、轻微服帖
hair.fringe: swept-back-side              # 侧后梳
hair.details:
  - visible_hairline
  - light_graying                         # ★ 少量白发
```

---

## 三、本档的影调（与青少年档不同）

青少年档是暖调、低对比、黄金时段。**本档是冷调、平光、办公荧光**——
这是"不同场景不同影调"的正确示范，不要混用。

```yaml
highlight_tint: 中性偏冷              # 窗光偏冷
shadow_tint: 中性灰偏冷
contrast: low-medium                 # 平淡，不是戏剧性对比
saturation: low                      # 比青少年档更低
lighting_nature: flat-diffused-cold  # ★ 平淡漫射冷光（办公环境）
lighting_source: 顶部荧光 + 侧窗     # 双光源混合，无戏剧性主光
rim_light: none                      # 完全没有
depth_of_field: medium               # 比青少年档景深浅一些
palette_environment: 深蓝/灰/米白/暗红文件夹  # 办公固有色
palette_wardrobe: 深navy + 白色细条纹
```

**值得学的一点**：这张图的"真实感"来自**平淡的光**，不是漂亮的光。
生成成年职业角色时，如果给戏剧性打光，会立刻变成广告片而不是剧照。

---

## 四、使用方法

当角色是**成年权威类**（家长/上司/校长/医生/警探）时：

1. 用本档的骨相与皮肤参数，**不要用青少年档**
2. **必须显式写年龄特征**（表情纹、颧下凹陷、眼下细节、发际线）
3. 负面层额外加：`不得磨皮`、`不得去除皱纹`、`不得逆龄处理`
4. 影调切到本档的冷调平光，**不要**用青少年档的暖调黄金时段
5. 妆容写 `clean-minimal`，并显式说明**不遮盖皱纹**

第 5 点容易被忽略：写了"淡妆"但没说"不遮皱纹"，模型会把妆当遮瑕用，年龄特征又没了。

---

## 五、这个档位对"整批一致性"的意义

有了青少年档 + 成年档，一个完整的剧组现在可以覆盖：

| 档位 | 对应角色 |
| --- | --- |
| `ref-2026-10` 青少年档 | 男女主、学生群像、配角 |
| `ref-2026-10` 少数派（4 类） | 冷艳对照、拉丁系、憨厚配角 |
| **本档 成年权威** | 家长、校长、上司、医生、警探 |

**影调按场景切换，但同一场景内全批统一**——家长出现在家里时用家庭场景的暖调，
出现在办公室时用办公场景的冷调。这是场景属性，不是角色属性。

---

## 六、仍缺的样本

- 成年**男性**权威角色（现有成年样本仅女性一张）
- 中年角色的**全身/服装**细节
- 反派气质样本
- 情绪激烈状态下的面部（现有图多为平静或克制表情）
