# -# 主動脈瓣偵測專案 (Aortic Valve Detection)

本專案使用 YOLOv12 框架進行醫療影像（主動脈瓣）的目標偵測。包含完整的資料預處理、模型訓練、以及符合競賽格式的預測結果輸出。

##  環境要求
* Python 3.10+
* CUDA 12.1 (建議)
* 主要套件：`torch`, `torchvision`, `ultralytics`

##  資料夾結構
程式會自動將原始資料整理為以下 YOLO 標準格式：
- `datasets/train/`: 訓練用影像與標籤 (Patient 1-40)
- `datasets/val/`: 驗證用影像與標籤 (Patient 41-45)
- `datasets/test/`: 內部測試用影像 (Patient 46-50)
- `datasets/predict/`: 競賽預測用影像總匯

##  使用說明

### 1. 資料準備
確保您的目錄下有 `training_image.zip` 與 `training_label.zip`。執行程式碼後，系統會自動解壓並過濾「無標註」的影像以進行優化訓練。

### 2. 模型訓練
預設使用 `yolo12n.pt` 預訓練權重。
- **解析度**: 640x640
- **Batch Size**: 16
- **Epochs**: 10 (可自行調整)

### 3. 預測與輸出
針對測試集進行預測後，結果會儲存於：
- **視覺化結果**: `runs/detect/predict/`
- **文字結果**: `./predict_txt/images.txt` (格式：`文件名 類別 信心度 x1 y1 x2 y2`)

## 驗證模型
使用以下指令可直接產出測試集的 mAP 評估報告：
```bash
yolo detect val model=runs/detect/train/weights/best.pt data=aortic_valve_colab.yaml split=test save_txt save_conf
