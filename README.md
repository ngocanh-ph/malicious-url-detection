# Malicious URL Detection

Phân loại URL độc hại thành 4 nhóm sử dụng Machine Learning và Deep Learning.  
Dataset: [Malicious URLs Dataset (Enhanced 2026)](https://www.kaggle.com/datasets/sid321axn/malicious-urls-dataset) - 651,191 URLs, 59 features.

---

## Kết quả

| Model | Accuracy | F1-macro | Input |
|---|---|---|---|
| **CNN** | **95.97%** | **94.77%** | Raw URL (char-level) |
| LSTM | 95.12% | 93.34% | Raw URL (char-level) |
| Random Forest | 92.63% | 90.27% | 59 engineered features |
| Neural Network (MLP) | 92.20% | 89.00% | 59 engineered features |
| KNN | 91.48% | 88.69% | 59 engineered features |
| Decision Tree (tuned) | 91.96% | 89.15% | 59 engineered features |
| SimpleRNN (improved) | 88.88% | 86.08% | Raw URL (char-level) |
| SVM | 84.53% | 70.16% | 59 engineered features |
| Logistic Regression | 84.37% | 70.42% | 59 engineered features |
| Naïve Bayes | 80.48% | 64.84% | 59 engineered features |
| SimpleRNN (baseline) | 66.06% | 21.10% | Raw URL (char-level) |

---

## Dataset

| Nhãn | Loại | Số lượng | Tỷ lệ |
|---|---|---|---|
| 0 | Benign | 428,103 | 65.7% |
| 1 | Defacement | 96,457 | 14.8% |
| 2 | Phishing | 94,111 | 14.5% |
| 3 | Malware | 32,520 | 5.0% |

**File CSV không được lưu trong repo** do giới hạn kích thước (147MB).  
Tải dataset tại: https://www.kaggle.com/datasets/sid321axn/malicious-urls-dataset  
Sau khi tải, đặt file vào thư mục gốc của project với tên `final_dataset_with_all_features_v3.1.csv`.

---

## Cấu trúc Project

```
malicious-url-detection/
│
├── README.md
├── requirements.txt
├── notebooks/
│   ├── 01_EDA.ipynb              # Phân tích khám phá dữ liệu
│   ├── 02_ML_models.ipynb        # 7 mô hình ML truyền thống
│   ├── 03_DL_models.ipynb        # CNN, LSTM, SimpleRNN
│   └── 04_improvements.ipynb     # Các kỹ thuật cải thiện
├── src/
│   ├── preprocessing.py          # Pipeline tiền xử lý
│   └── evaluate.py               # Hàm đánh giá model
└── results/
    ├── figures/                  # Biểu đồ, confusion matrix
    └── summary_results.csv       # Bảng kết quả tổng hợp
```

---

## Hai Pipeline Dữ Liệu

Project sử dụng 2 pipeline riêng biệt, phản ánh sự khác nhau căn bản giữa mô hình ML và DL:

**`df_tab`: dành cho ML truyền thống**  
Giữ lại 59 features số. Loại bỏ các cột text (`url`, `domain`, `scan_date`). Chuẩn hóa bằng `StandardScaler` fit trên train, transform trên test (tránh data leakage).

**`df_seq`: dành cho Deep Learning**  
Giữ lại raw URL string. Tokenize ở cấp độ ký tự (`char_level=True`), pad/truncate về độ dài 200. Cho phép CNN và LSTM học trực tiếp từ pattern ký tự trong URL như `/login`, `.exe`, `@`, `//`.

---

## Các Kỹ Thuật Cải Thiện

[Đang trong thời gian update]

---

## Cài Đặt

```bash
git clone https://github.com/ngocanh-ph/malicious-url-detection.git
cd malicious-url-detection
pip install -r requirements.txt
```

Tải dataset từ Kaggle, đặt vào thư mục gốc, sau đó chạy các notebook theo thứ tự từ `01` đến `04`.

---