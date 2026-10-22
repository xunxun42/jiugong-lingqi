# 立绘生成模板 v2（本地 SDXL 版）

模型：**Animagine XL 4.0**（SDXL 二次元，SDXL 1024×1024）
生成：本地 ComfyUI 127.0.0.1:8188，约 30 秒/张
处理：居中方形裁切 → 512×512 → webp q88（33–70 KB/张）

## 为什么换掉 v1（智谱 cogview-3-flash）

| | cogview-3-flash | Animagine XL 4.0 |
|---|---|---|
| 线条 | 糊、软 | 清晰黑勾线、赛璐璐平涂 |
| 脸 | 平面化、五官飘 | 结构稳、眼睛有设计感 |
| 背景 | 常跑成亮色 | 深色渐变稳定可控 |
| 出片率 | 常要重抽 | 4 张里 3 张可用 |

## 正向提示词模板

本模型吃 **Danbooru 英文标签**，不要写中文（中文描述效果会掉一档）。

`
1girl/1boy, solo, upper body, portrait, looking at viewer,
<发色发型>, <瞳色>, fair skin, warm skin tone,
<服装细节>, <元素特效>, <元素粒子>,
dark <元素> gradient background, vignette,
cinematic lighting, rim light, well lit face,
cel shading, flat color, clean lineart, anime style,
masterpiece, best quality, very aesthetic
`

## 负向提示词

`
lowres, bad anatomy, bad hands, extra digits, fewer digits, missing fingers,
text, watermark, signature, username, artist name, logo,
worst quality, low quality, low score, bad score, average score,
realistic, photorealistic, 3d, cgi, blurry, jpeg artifacts, cropped, out of frame,
multiple girls, chibi,
bright background, white background, light background, pastel colors,
high key lighting, low key lighting, underexposed, dark face, grey skin,
simple background, outdoors, sky
`

## 参数

1024×1024 · 30 steps · CFG 6.5 · dpmpp_2m + karras · seed 固定可复现

## 踩过的坑（实测）

| 问题 | 原因 | 对策 |
|---|---|---|
| 背景跑成亮色 | 只写 dark background 会被忽略 | 正向写 dark <元素> gradient background，**同时在负向压 right/white/light background** |
| 人脸压成灰色 | 用了 low key lighting / deep shadows | 删掉它们，改成 im light + well lit face：只压背景、不打压人物 |
| 皮肤发灰 | 缺肤色锚点 | 正向加 air skin, warm skin tone |
| 中文提示词没效果 | 模型只认 Danbooru 标签 | 全部改英文标签 |

## 处理流程

1. ComfyUI 出图 1024×1024 → C:\Users\Public\ComfyUI\out\
2. uild_assets.py 批量：居中裁切 → 512×512 → webp q88 → ssets/spirits/{id}.webp
3. 文件名与代码里 rt 字段一一对应，替换即生效，**不需要改任何代码**

## 分组约定

- **服装统一**：黑色皮衣体系（立领 / 露肩 / 护肩 / 兜帽 / 毛领）
- **构图统一**：半身、居中、面部与肩膀完整可见
- **背景统一**：深色渐变 + 元素粒子（火光 / 冰晶 / 水泡 / 风羽 / 碎石 / 藤叶 / 星屑 / 暗影）
- **画风锁死**：赛璐璐平涂 + 黑色勾线 + 单层阴影，禁写实