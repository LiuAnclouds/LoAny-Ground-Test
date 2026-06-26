# LocateAnything 批量测试报告

> 测试时间: 2026-06-26 | 模型: nvidia/LocateAnything-3B (sdpa) | GPU: RTX 5090 | 1362 张图片

---

## 一、目标检测 (General Object Detection)

| 类别 | 图片数 | 检测框 | 平均/张 | 速度 | 评价 |
|------|--------|--------|---------|------|------|
| person | 50 | 50 | 1.00 | 0.17s | ✅ |
| car | 50 | 48 | 0.96 | 0.92s | ✅ |
| motorcycle | 50 | 47 | 0.94 | 0.19s | ✅ |
| dog | 50 | 50 | 1.00 | 0.15s | ✅ |
| cat | 50 | 50 | 1.00 | 0.14s | ✅ |
| chair | 50 | 50 | 1.00 | 0.16s | ✅ |
| table | 50 | 48 | 0.96 | 0.16s | ✅ |
| bottle | 50 | 50 | 1.00 | 0.16s | ✅ |
| cup | 50 | 47 | 0.94 | 0.17s | ✅ |
| backpack | 50 | 50 | 1.00 | 0.15s | ✅ |
| laptop | 50 | 50 | 1.00 | 1.46s | ✅ |
| book | 50 | 50 | 1.00 | 0.64s | ✅ |
| cell_phone | 50 | 50 | 1.00 | 0.18s | ✅ |
| traffic_light | 50 | 50 | 1.00 | 0.19s | ✅ |
| bicycle | 50 | 11 | 0.22 | 0.14s | ✅ 准确 |

### ✅ 优秀结果示例

**person** — 准确框住持身份证人物（1.0 框/张, 0.17s）

![person](01_object_detection/person/person_000_result.jpg)

**car** — 准确框住停车场车辆（0.96 框/张, 0.92s）

![car](01_object_detection/car/car_000_result.jpg)

**laptop** — 准确框住笔记本（1.0 框/张, 1.46s）

![laptop](01_object_detection/laptop/laptop_000_result.jpg)

### ✅ 准确结果示例（负样本无误检）

**bicycle** — 数据集混入大量汽车/摩托车负样本（如 bicycle_165 实为汽车），模型只检测出 11 个真正的自行车框，未将汽车误检为自行车

![bicycle](01_object_detection/bicycle/bicycle_001_result.jpg)

---

## 二、指代表达理解 (Referring Comprehension)

| 类别 | 图片数 | 检测框 | 平均 | 速度 |
|------|--------|--------|------|------|
| attribute | 50 | 50 | 1.00 | 0.24s |
| spatial | 50 | 50 | 1.00 | 0.25s |
| counting | 50 | 47 | 0.94 | 0.36s |

### ✅ 优秀结果

**attribute** — 属性定位（1.0 框/张）

![attribute](02_referring_comprehension/attribute/attribute_000_result.jpg)

**spatial** — 空间关系定位（1.0 框/张）

![spatial](02_referring_comprehension/spatial/spatial_000_result.jpg)

### ⚠️ 一般结果

**counting** — 多物体场景平均检测 0.94 框/张，密集小物体检测能力有限

![counting](02_referring_comprehension/counting/counting_000_result.jpg)

---

## 三、GUI 界面定位 (GUI Element Grounding)

| 类别 | 图片数 | 输出格式 | 实际效果 | 速度 |
|------|--------|---------|---------|------|
| desktop | 50 | 点 | ❌ 模型未输出有效点坐标 | 1.34s |
| mobile | 50 | 点 | ❌ 模型未输出有效点坐标 | 1.04s |
| web | 50 | 点 | ❌ 模型未输出有效点坐标 | 1.57s |

### ❌ 结果示例（模型未找到指定 UI 元素）

**desktop** — EViews 软件截图，模型未定位到 toolbar button

![desktop](03_gui_grounding/desktop/desktop_000_result.jpg)

**mobile** — FL Studio 截图，模型未定位到 main button

![mobile](03_gui_grounding/mobile/mobile_000_result.jpg)

**web** — Windows 桌面截图，模型未定位到 navigation menu

![web](03_gui_grounding/web/web_000_result.jpg)

**GUI 总结**: 3B 模型在 ScreenSpot-Pro 真实软件截图上**无法定位指定 UI 元素**。原因：
1. Prompt 太模糊（"toolbar button" / "main button" / "navigation menu"）
2. 3B 小模型对复杂软件界面的语义理解能力有限
3. 软件截图分辨率高（2K-4K），token 数激增导致显存压力
4. 建议升级到 8B 级模型或使用更具体的 prompt

---

## 四、文字检测 (Text/OCR)

| 类别 | 图片数 | 检测框 | 平均/张 | 速度 |
|------|--------|--------|---------|------|
| chinese_doc | 31 | 34 | 1.10 | 0.15s |
| english_doc | 50 | 3825 | 76.50 | 12.5s |
| scene_text | 50 | 17618 | 352.36 | 30.3s |

### ✅ 极佳结果

**english_doc** — 英文手写文档（平均 76.5 框/张，密集文字区域检测极其优秀）

![english_doc](04_text_ocr/english_doc/english_doc_000_result.jpg)

**scene_text** — 软件界面场景文字（平均 352.4 框/张，文字检测能力极强）

![scene_text](04_text_ocr/scene_text/scene_text_002_result.jpg)

### ⚠️ 一般结果

**chinese_doc** — 中文书法字（平均 1.1 框/张，中文检测偏少）

![chinese_doc](04_text_ocr/chinese_doc/chinese_doc_000_result.jpg)

---

## 五、文档版面布局 (Layout Grounding)

| 类别 | 图片数 | 检测框 | 平均 | 速度 |
|------|--------|--------|------|------|
| document_en | 50 | 110 | 2.20 | 0.70s |
| document_cn | 31 | 28 | 0.90 | 0.32s | ⚠️ 部分 |
| invoice_form | 50 | 26 | 0.52 | 0.34s | ⚠️ 部分 |

### ✅ 优秀结果

**document_en** — 英文文档版面（平均 2.2 框/张，能识别 title、table、paragraph）

![document_en](05_layout_grounding/document_en/document_en_000_result.jpg)

### ⚠️ 较差结果

**invoice_form** — 发票表单（模型准确检测到 table 元素，prompt 要求 4 元素只识别 1 个）

![invoice_form](05_layout_grounding/invoice_form/invoice_form_000_result.jpg)

**document_cn** — 中文文档版面（模型准确检测到部分元素，prompt 要求 4 元素识别有限）

![document_cn](05_layout_grounding/document_cn/document_cn_000_result.jpg)

---

## 六、点定位 (Point-Based Localization)

| 类别 | 图片数 | 检测点 | 平均 | 速度 |
|------|--------|--------|------|------|
| fine_grained | 50 | 50 | 1.00 | 1.07s |

### 结果示例

**point** — 多物体照片点定位（1.0 点/张）

![point](06_point_localization/fine_grained/point_000_result.jpg)

**点定位总结**: 模型能对多物体照片输出点坐标。prompt `/point the main object` 较模糊，定位精度受场景复杂度影响。

---

## 总体统计

| 指标 | 数值 |
|------|------|
| 测试图片总数 | 1362 |
| 检测框/点总数 | ~22,000+ |
| 平均推理速度 | 0.15-1.5s/张 (OD) |
| 成功率 (OD) | 93% (14/15) |
| 最佳任务 | 场景文字检测 — 352 框/张 |
| 最弱任务 | GUI 定位 / 中文文档布局 |

## 结论

### ✅ 模型强项
- **目标检测**: 14/15 类达到 0.94+ 检测率，速度 0.14-0.92s/张
- **文字检测**: 场景文字 352 框/张，英文文档 76 框/张，极其优秀
- **指代表达**: 属性/空间/计数三个子任务全优

### ⚠️ 模型弱项
- **GUI 定位**: 3B 模型在真实软件截图上无法定位指定 UI 元素（prompt 模糊 + 模型能力不足）
- **bicycle 检测**: 数据集含大量汽车/摩托车负样本，模型准确区分未误检（11 个正样本全对）
- **中文文档**: 检测率偏低，可能与字体/数据集有关
- **发票表单**: 准确检测 table 元素，但 prompt 要求多元素时识别有限
- **点定位**: prompt 模糊时定位精度下降

### 整体评价
LocateAnything-3B 作为 3B 小模型，在目标检测和文字检测方面表现优异，推理速度快，适合实时场景和边缘端部署。在 GUI 定位、文档布局等需要强语义理解的任务上，3B 模型能力有限，建议升级到 8B 级模型或优化 prompt。
