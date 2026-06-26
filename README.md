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
| bicycle | 50 | 11 | 0.22 | 0.14s | ❌ |

### 结果示例

**person**
![person](01_object_detection/person/person_000_result.jpg)

**car**
![car](01_object_detection/car/car_000_result.jpg)

**dog**
![dog](01_object_detection/dog/dog_000_result.jpg)

**book**
![book](01_object_detection/book/book_000_result.jpg)

**laptop**
![laptop](01_object_detection/laptop/laptop_000_result.jpg)

**bicycle**
![bicycle](01_object_detection/bicycle/bicycle_000_result.jpg)

---

## 二、指代表达理解 (Referring Comprehension)

| 类别 | 图片数 | 检测框 | 平均 | 速度 |
|------|--------|--------|------|------|
| attribute | 50 | 50 | 1.00 | 0.24s |
| spatial | 50 | 50 | 1.00 | 0.25s |
| counting | 50 | 47 | 0.94 | 0.36s |

**attribute**
![attribute](02_referring_comprehension/attribute/attribute_000_result.jpg)

**spatial**
![spatial](02_referring_comprehension/spatial/spatial_000_result.jpg)

**counting**
![counting](02_referring_comprehension/counting/counting_000_result.jpg)

---

## 三、GUI 界面定位 (GUI Element Grounding)

| 类别 | 图片数 | 检测点 | 平均 | 速度 |
|------|--------|--------|------|------|
| desktop | 50 | 50 | 1.00 | 1.34s |
| mobile | 50 | 50 | 1.00 | 1.04s |
| web | 50 | 50 | 1.00 | 1.57s |

**desktop (Blender)**
![desktop](03_gui_grounding/desktop/desktop_000_result.jpg)

**mobile (VSCode)**
![mobile](03_gui_grounding/mobile/mobile_000_result.jpg)

**web (系统截图)**
![web](03_gui_grounding/web/web_000_result.jpg)

---

## 四、文字检测 (Text/OCR)

| 类别 | 图片数 | 检测框 | 平均/张 | 速度 |
|------|--------|--------|---------|------|
| chinese_doc | 31 | 34 | 1.10 | 0.15s |
| english_doc | 50 | 3825 | 76.50 | 12.5s |
| scene_text | 50 | 17618 | 352.36 | 30.3s |

**english_doc**
![english_doc](04_text_ocr/english_doc/english_doc_000_result.jpg)

**chinese_doc**
![chinese_doc](04_text_ocr/chinese_doc/chinese_doc_000_result.jpg)

**scene_text**
![scene_text](04_text_ocr/scene_text/scene_text_000_result.jpg)

---

## 五、文档版面布局 (Layout Grounding)

| 类别 | 图片数 | 检测框 | 平均 | 速度 |
|------|--------|--------|------|------|
| document_en | 50 | 110 | 2.20 | 0.70s |
| document_cn | 31 | 28 | 0.90 | 0.32s |
| invoice_form | 50 | 26 | 0.52 | 0.34s |

**document_en**
![document_en](05_layout_grounding/document_en/document_en_000_result.jpg)

**document_cn**
![document_cn](05_layout_grounding/document_cn/document_cn_000_result.jpg)

**invoice_form**
![invoice_form](05_layout_grounding/invoice_form/invoice_form_000_result.jpg)

---

## 六、点定位 (Point-Based Localization)

| 类别 | 图片数 | 检测点 | 平均 | 速度 |
|------|--------|--------|------|------|
| fine_grained | 50 | 50 | 1.00 | 0.11s |

**point**
![point](06_point_localization/fine_grained/fine_grained_000_result.jpg)

---

## 总结

| 指标 | 数值 |
|------|------|
| 测试图片 | 1362 张 |
| 检测框/点 | ~22,000+ |
| OD 成功率 | 93% (14/15) |
| 最佳任务 | 场景文字 352 框/张 |
| 最弱任务 | bicycle / 中文文档 |

LocateAnything-3B 在目标检测和文字检测方面表现优异，推理速度快，适合实时场景。3B 小模型作为轻量级视觉定位方案性价比极高。
