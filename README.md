# AntiFraud 金融詐騙風險偵測系統

## 專案簡介
本專案聚焦於**金融詐騙對話自動斷詞、關鍵字標註與理論階段分類**，結合 Hugging Face `ckiplab/bert-base-chinese-ws` 斷詞模型與學術詐騙流程理論，協助自動化偵測高風險詐騙訊息。

## 主要功能
- **中文斷詞與關鍵字標註**：自動辨識金融詐騙高風險詞彙。
- **理論階段分類**：依據詐騙七階段/五階段理論，自動分類對話所屬詐騙流程。
- **模型微調**：支援 BIO 格式資料自動微調，強化金融詐騙語境。
- **批次推論與報告**：可對大量對話資料自動批次分析與分類。
- **單元測試**：高覆蓋率 pytest 測試，確保斷詞與關鍵字偵測品質。

## 安裝與環境建議

建議使用 Python 3.10+，可用 venv/conda 建立虛擬環境。

```bash
# 建立虛擬環境
python -m venv venv
# 啟動虛擬環境
source venv/bin/activate  # Windows: venv\Scripts\activate
# 安裝依賴
pip install -r requirements.txt
```

必要套件：
- ckip-transformers>=0.3.2
- transformers>=4.0.0
- torch>=1.7.0
- datasets>=2.0.0

## 目錄結構

```
AntiFraud/
├── src/
│   ├── infer_ws.py                # 單句斷詞與關鍵字推論
│   ├── batch_infer.py             # 批次推論與理論階段分類
│   ├── finetune_ws.py             # 斷詞模型微調腳本
│   ├── word_segmentation_eval.py  # 斷詞與關鍵字自動評估
│   ├── theory_stage_classifier.py # 理論階段分類模組
│   └── finetuned_ws/              # 微調後模型與 tokenizer
├── data/
│   └── ws_finetune_sample.txt     # BIO 格式微調資料範例
├── tests/
│   └── test_word_segmentation_eval.py # 單元測試
├── requirements.txt
├── README.md
├── LICENSE
└── InitProject.bat                # Windows 初始化腳本
```

## 使用方式

### 1. 斷詞與關鍵字推論
```bash
python src/infer_ws.py
```
- 輸出每句話的斷詞與關鍵字標註。

### 2. 批次推論與理論階段分類
```bash
python src/batch_infer.py
```
- 批次分析對話檔案，並自動分類詐騙階段。

### 3. 斷詞模型微調
```bash
python src/finetune_ws.py
```
- 需先準備 BIO 格式資料於 `data/ws_finetune_sample.txt`。

### 4. 斷詞與關鍵字自動評估
```bash
python src/word_segmentation_eval.py
```
- 自動統計關鍵字命中率，給出微調建議。

### 5. 單元測試
```bash
pytest tests/
```

## 資料格式說明
`data/ws_finetune_sample.txt` 範例：
```
寶 O
貝 O
匯 B-KEYWORD
款 I-KEYWORD
...
```
空行分隔句子，B-KEYWORD/I-KEYWORD 為關鍵字標註。

## 授權
MIT License
