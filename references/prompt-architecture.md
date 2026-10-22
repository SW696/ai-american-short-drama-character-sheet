# 提示词架构：七层语法

角色卡 → 提示词是**确定性编译**，不是二次创作。层序不可调换，因为主流生图模型对
前部 token 权重更高：越靠前的层越"不可被推翻"。

## 层序

| 层 | 内容 | 作用 | 可否省 |
| --- | --- | --- | --- |
| L1 媒介与写实度 | 真人写实电影级人物设定图、高写实、真实真人摄影质感 | 定基调，压住插画/CG 倾向 | 不可 |
| L2 版式与视图契约 | 纯白无缝背景、左特写/右全身、同一人、无文字 | 定构图，这类图的核心 | 不可 |
| L3 身份锚 | 骨相 → 眼 → 眉 → 鼻 → 唇 → 皮肤 | 定"是谁"，必须逐字复用 | 不可 |
| L4 造型锚 | 发型（色/长/量/轮廓/层次/刘海/侧后） | 定"像不像同一人" | 不可 |
| L5 服装 | 类别 + 主辅色 + 版型 + 细节 + 配件 | 易变层 | 可省（改为实景时装） |
| L6 摄影技术 | 镜头、光圈、光位、姿态、眼神、皮肤质感 | 定"拍得像不像真的" | 不可 |
| L7 负面约束 | 基础集 + 分类集 | 兜底 | 不可 |

**L3 内部顺序**也必须固定：骨相 → 眼 → 眉 → 鼻 → 唇 → 皮肤。
理由：先定"脸的形状"再定"脸上的零件"，模型不会因为描述后段而改动前段的骨架。

---

## 中文提示词骨架（可直接投喂，按需替换 `{}`）

```
{L1}：真人写实电影级人物设定图，纯白色无缝背景，同一名{年龄}{族裔}{性别}，
左右人物的面部特征、发型、肤色、服装完全一致。
{L2}：左侧为人物正面面部近距离特写，右侧为正面全身站立视图，人物自然平视镜头，
标准站姿，无文字。
{L3}：约{年龄}岁，身材高挑修长，肩颈线条优越，锁骨清晰，整体气质带有{气质描述}；
肤色{tone}，保留真实自然皮肤纹理和{finish}，脸型为{face_shape}，面部轮廓流畅清晰，
下颌线{jawline}，下巴{chin}，颧骨{cheekbones}，眉骨{brow_ridge}；
五官高度精致，眼睛为{eye_color}，眼型{eye_shape}，眼神{gaze}；
眉毛{density}，眉形{shape}，颜色为{brow_color}，与发色协调但仍保留一定存在感；
鼻梁{bridge}，鼻头{tip}，嘴唇{fullness}，唇峰{cupids_bow}，嘴角{corners}，{facial_hair}。
{L4}：{hair_length}，发量{volume}，整体轮廓{silhouette}，带明显层次与{messiness}感，
顶部{top}，前额{fringe}，两侧和后侧{sides_back}，发丝柔软，保留自然空气感。
{L5}：身穿{category 中文描述}，{palette}配色，版型{fit}，{detail}；
手腕佩戴{accessories}，脚穿{socks_shoes}。
{L6}：左侧特写重点表现{left_focus}；右侧完整显示头顶至鞋底，双手自然垂落，
摄影棚柔和均匀布光，{lens}，{aperture}，高写实、高细节、真实真人摄影质感。
```

注：`身材高挑修长、肩颈线条优越、锁骨清晰` 属**编译层恒定身材句**，不落角色卡——
它对全批角色都成立，落卡会造成重复并削弱批次统一性。

## 英文提示词骨架（供英文优先的模型）

```
{L1} Photorealistic cinematic live-action character reference sheet, seamless pure white
background, one single {age} {ethnicity} {gender}, all features identical across both views.
{L2} Left: close-up frontal face portrait. Right: full-body frontal standing view, gaze
naturally level with camera, standard standing pose, no text or lettering anywhere.
{L3} Face: {face_shape} face, clean flowing contours, {jawline} jawline, {chin} chin,
{cheekbones} cheekbones, {brow_ridge} brow ridge. Eyes: {eye_color}, {eye_shape},
{gaze} expression, {brow_density} clearly-defined {brow_color} brows. Nose: {bridge}
bridge, {nose_tip} tip. Lips: {fullness}, {cupids_bow} cupid's bow, {corners} corners.
{facial_hair}. Skin: {tone}, {texture}, {finish}.
{L4} Hair: {hair_color}, {hair_length}, {volume} volume, {silhouette} silhouette,
{layers} layers, {messiness} texture, {top} top, {fringe} fringe, {sides_back} sides
and back, soft strands retaining natural airiness.
{L5} Wardrobe: {garment description}, {palette} palette, {fit} fit, {detail}.
{L6} Left view emphasizes {left_focus}. Right view shows head to sole, arms hanging
naturally. Soft even studio lighting, {lens}, {aperture}, high realism, high detail,
authentic live-action photographic quality.
{L7} Negative: {negative joined by comma}
```

---

## 三个关键编译规则

**1. 一致性靠"显式声明"承接，不靠重复名词。**
L2 里那句「左右人物的面部特征、发型、肤色、服装完全一致」是整张图成败的锚点句，
不可省略。仅在两处分别描述同一个人，模型并不认为它们是同一人。

**1b. 同角色的第二张图，L3–L4 必须逐字复制。**
这是纯文本模式（无垫图）下唯一的一致性手段。**严禁重新措辞**：
"下颌线锋利干净" 改写成 "下颌线条清晰锐利"，含义相同但模型视为两句不同的话。
正确做法是把 L3–L4 当作一整块不可编辑的文本块保存，每次原样粘贴。

**2. 特写要"点名交付物"。**
左视图不能只说"特写"。必须列出证据项：
`浅色瞳孔、立体眉眼、挺直鼻梁、清晰唇形、真实皮肤细节`。
不点名，模型就会把近距离画成一张普通正面照。

**3. 全身要"点名边界"。**
右视图必须写 `完整显示头顶至鞋底`，否则**脚被裁掉**是最常见的失败模式。
同时写"双手自然垂落"可显著降低手部畸形率。

---

## 负面层编译

把角色卡的 `negative` 列表翻译成**该后端实际支持的字段**：

- 后端有独立负面提示词字段（`negative_prompt` / `--no` 等，名称以 `schema` 为准）→ 填入逗号连接列表
- 后端只有单一提示词字段 → 写成否定句，追加在提示词末尾：

```
画面中不得出现任何文字、字母、水印、签名、logo；不得出现第二个人；
左右两张脸必须是同一个人；不得裁切头顶与脚部；不得出现胡须、眼镜、
塑料感磨皮皮肤；手部不得畸形或有多余手指。
```

```
no text, no letters, no words, no watermark, no signature, no logo,
no additional person, no duplicate face, no mismatched faces between views,
no cropped feet, no cropped head, no deformed hands, no extra fingers,
no plastic skin, no over-smoothed, no airbrushed
```

**禁止凭记忆猜字段名或 `--no` 语法**——一律以已安装二进制的 `schema` 输出为准。

---

## 常见编译错误

| 错误 | 后果 | 修正 |
| --- | --- | --- |
| L3 与 L4 之间插入服装 | 骨架被服装 token 干扰，脸型漂移 | 服装固定放 L5 |
| 用 "8K, ultra detailed, masterpiece, best quality" 堆量 | 塑料假脸，与"真实质感"冲突 | 删掉，改用具体可验证要求（毛孔、细纹、皮肤纹理） |
| 负面要求只写在正面句里（"无文字"） | 模型忽略否定 | 独立写入 L7 |
| 两个视图分别写了不一致的形容词 | 左右脸不同 | 身份锚只写一次，全图共用 |
| 特写视图写"全身"或全身视图写"半身" | 视图契约自相矛盾 | 严格按 viewSpec |
