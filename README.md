# Dự Án Phân Tích và Dự Đoán Đột Quỵ (Stroke Prediction Analysis)

## Thông Tin Nhóm

### Thành viên
- **Thành viên 1**: [Họ tên] - [MSSV] - [Email]
  - Phân công: [Các task đảm nhận]
  - Đóng góp: [%]

- **Thành viên 2**: [Họ tên] - [MSSV] - [Email]
  - Phân công: [Các task đảm nhận]
  - Đóng góp: [%]

- **Thành viên 3**: [Họ tên] - [MSSV] - [Email]
  - Phân công: [Các task đảm nhận]
  - Đóng góp: [%]

### Quy trình làm việc nhóm
- **Công cụ collaboration**: [GitHub/Google Drive/etc.]
- **Họp nhóm**: [Lịch họp]
- **Phân chia công việc**: [Mô tả cách phân chia]

---

## Tổng Quan Dự Án

### Giới thiệu
Dự án này thực hiện phân tích toàn diện về dữ liệu y tế liên quan đến đột quỵ (stroke), nhằm:
- Khám phá các yếu tố nguy cơ chính gây đột quỵ
- Xây dựng mô hình Machine Learning dự đoán nguy cơ đột quỵ
- Đưa ra những insights có giá trị cho việc phòng ngừa và điều trị

### Ý nghĩa thực tiễn
Theo Tổ chức Y tế Thế giới (WHO), đột quỵ là nguyên nhân gây tử vong đứng thứ 2 trên toàn cầu, chiếm khoảng 11% tổng số ca tử vong. Việc phát hiện sớm và dự đoán nguy cơ đột quỵ có thể:
- Cứu sống hàng triệu người
- Giảm tỷ lệ tàn tật
- Tiết kiệm chi phí y tế
- Cải thiện chất lượng cuộc sống

---

## Dataset - Bộ Dữ Liệu

### Nguồn dữ liệu
- **Platform**: Kaggle
- **Tên dataset**: Stroke Prediction Dataset
- **URL**: https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset
- **Tác giả**: fedesoriano
- **Giấy phép**: Chỉ sử dụng cho mục đích giáo dục (Educational use only)
- **Ngày thu thập**: [Cập nhật sau khi kiểm tra]

### Mô tả dataset
- **Kích thước**: [X] hàng × 12 cột
- **Dung lượng**: [X] MB
- **Mỗi hàng đại diện**: Một bệnh nhân (patient record)
- **Định dạng**: CSV

### Các cột dữ liệu (Features)

| Tên cột | Ý nghĩa (Tiếng Việt) | Kiểu dữ liệu | Ghi chú |
|---------|---------------------|--------------|---------|
| `id` | Mã định danh bệnh nhân | Integer | Unique identifier |
| `gender` | Giới tính | Categorical | Male/Female/Other |
| `age` | Tuổi | Numeric | Năm |
| `hypertension` | Tình trạng tăng huyết áp | Binary | 0 = Không, 1 = Có |
| `heart_disease` | Bệnh tim | Binary | 0 = Không, 1 = Có |
| `ever_married` | Tình trạng hôn nhân | Categorical | Yes/No |
| `work_type` | Loại công việc | Categorical | children/Govt_job/Never_worked/Private/Self-employed |
| `Residence_type` | Nơi cư trú | Categorical | Urban (Thành thị)/Rural (Nông thôn) |
| `avg_glucose_level` | Mức đường huyết trung bình | Numeric | mg/dL |
| `bmi` | Chỉ số khối cơ thể (Body Mass Index) | Numeric | kg/m² |
| `smoking_status` | Tình trạng hút thuốc | Categorical | formerly smoked/never smoked/smokes/Unknown |
| `stroke` | Đột quỵ (TARGET) | Binary | 0 = Không, 1 = Có |

### Phương pháp thu thập
- **Nguồn**: Hồ sơ y tế bệnh nhân (confidential medical records)
- **Loại dữ liệu**: Clinical/Administrative data
- **Đặc điểm**: Dữ liệu thực tế từ bệnh viện/phòng khám
- **Hạn chế**: Không rõ khu vực địa lý, khoảng thời gian thu thập cụ thể

---

## Câu Hỏi Nghiên Cứu (Research Questions)

### Danh sách câu hỏi
[Sẽ cập nhật sau khi xác định số thành viên nhóm - cần 2×n câu hỏi]

1. **[Q1] - Phân tích nhân khẩu học và yếu tố nguy cơ**
   - Nội dung: [Sẽ bổ sung]
   - Loại phân tích: Descriptive/Statistical

2. **[Q2] - Ảnh hưởng của lối sống**
   - Nội dung: [Sẽ bổ sung]
   - Loại phân tích: Analytical

3. **[Q3] - Mối liên hệ đường huyết và đột quỵ**
   - Nội dung: [Sẽ bổ sung]
   - Loại phân tích: Statistical

4. **[Q4] - Yếu tố địa lý và xã hội**
   - Nội dung: [Sẽ bổ sung]
   - Loại phân tích: Exploratory

5. **[Q5] - Mô hình Machine Learning dự đoán đột quỵ** ⭐ **(BẮT BUỘC)**
   - Nội dung: [Sẽ bổ sung]
   - Loại phân tích: Machine Learning

6. **[Q6] - [Tùy thuộc số thành viên]**
   - Nội dung: [Sẽ bổ sung]
   - Loại phân tích: [Sẽ bổ sung]

---

## Kết Quả Chính (Key Findings)

[Sẽ cập nhật sau khi hoàn thành phân tích]

1. **[Finding 1]**: [Mô tả ngắn gọn]
2. **[Finding 2]**: [Mô tả ngắn gọn]
3. **[Finding 3]**: [Mô tả ngắn gọn]
4. **[Finding 4]**: [Mô tả ngắn gọn]
5. **[Finding 5]**: [Mô tả ngắn gọn]

### Phát hiện nổi bật nhất
[Insight thú vị/bất ngờ nhất từ phân tích]

### Kết quả mô hình ML

| Mô hình | ROC-AUC | Precision | Recall | F1-Score |
|---------|---------|-----------|--------|----------|
| [Model 1] | [X.XX] | [X.XX] | [X.XX] | [X.XX] |
| [Model 2] | [X.XX] | [X.XX] | [X.XX] | [X.XX] |
| [Model 3] | [X.XX] | [X.XX] | [X.XX] | [X.XX] |

**Mô hình tốt nhất**: [Tên model] với ROC-AUC = [X.XX]

---

## Cấu Trúc Dự Án (Project Structure)

```
ĐỒ ÁN CUỐI KÌ/
│
├── data/                          # Thư mục chứa dữ liệu
│   ├── healthcare-dataset-stroke-data.csv   # Dataset gốc
│   └── processed/                 # Dữ liệu đã xử lý (nếu có)
│
├── notebooks/                     # Thư mục chứa Jupyter Notebooks
│   └── stroke_analysis.ipynb     # Notebook phân tích chính
│
├── src/                          # Thư mục chứa source code (nếu có)
│   ├── utils.py                  # Hàm tiện ích
│   └── models.py                 # Các mô hình ML tùy chỉnh
│
├── CSC17104_2025_Final Project (1).pdf  # File yêu cầu đồ án
├── README.md                     # File này
└── requirements.txt              # Danh sách thư viện cần cài đặt
```

---

## Hướng Dẫn Chạy Dự Án (How to Run)

### Bước 1: Cài đặt môi trường

#### Yêu cầu hệ thống
- Python 3.8 trở lên
- Jupyter Notebook hoặc JupyterLab
- RAM tối thiểu: 4GB
- Dung lượng ổ cứng: 500MB

#### Cài đặt thư viện
```bash
# Cài đặt tất cả dependencies
pip install -r requirements.txt

# Hoặc cài đặt từng thư viện
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

### Bước 2: Tải dữ liệu
1. Truy cập: https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset
2. Tải file `healthcare-dataset-stroke-data.csv`
3. Đặt file vào thư mục `data/`

### Bước 3: Chạy Notebook
```bash
# Khởi động Jupyter Notebook
jupyter notebook

# Hoặc sử dụng JupyterLab
jupyter lab
```

Sau đó:
1. Mở file `notebooks/stroke_analysis.ipynb`
2. Chạy tất cả cells từ đầu đến cuối (Run All)
3. Thời gian chạy ước tính: ~5-10 phút (tùy cấu hình máy)

---

## Dependencies - Thư Viện Sử Dụng

### Core Libraries (Thư viện cốt lõi)
- `pandas` - Xử lý và phân tích dữ liệu
- `numpy` - Tính toán số học
- `matplotlib` - Vẽ biểu đồ cơ bản
- `seaborn` - Vẽ biểu đồ thống kê nâng cao

### Machine Learning
- `scikit-learn` - Các thuật toán ML, preprocessing, evaluation
- `imbalanced-learn` - Xử lý dữ liệu mất cân bằng (SMOTE)
- `xgboost` - Thuật toán Gradient Boosting

### Advanced Analysis
- `shap` - Giải thích mô hình ML (SHAP values)
- `scipy` - Kiểm định thống kê

### Utilities
- `jupyter` - Môi trường notebook
- `ipywidgets` - Tương tác trong notebook

Chi tiết phiên bản: xem file [requirements.txt](requirements.txt)

---

## Hạn Chế Của Dự Án (Limitations)

[Sẽ cập nhật sau khi phân tích]

1. **Dữ liệu**:
   - [Limitation 1]
   - [Limitation 2]

2. **Phương pháp phân tích**:
   - [Limitation 3]
   - [Limitation 4]

3. **Phạm vi nghiên cứu**:
   - [Limitation 5]

---

## Hướng Phát Triển Tương Lai (Future Work)

[Sẽ cập nhật sau khi phân tích]

1. **Câu hỏi bổ sung**: [Các câu hỏi muốn khám phá thêm]
2. **Phân tích sâu hơn**: [Phương pháp nâng cao]
3. **Dữ liệu bổ sung**: [Loại dữ liệu cần thêm]
4. **Cải tiến mô hình**: [Hướng tối ưu hóa]
5. **Ứng dụng thực tế**: [Deployment possibilities]

---

## Tài Liệu Tham Khảo (References)

1. World Health Organization (WHO). "The top 10 causes of death." https://www.who.int/news-room/fact-sheets/detail/the-top-10-causes-of-death

2. Kaggle Dataset: https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset

3. [Thêm các tài liệu tham khảo khác trong quá trình thực hiện]

---

## Liên Hệ (Contact)

Nếu có câu hỏi hoặc góp ý về dự án, vui lòng liên hệ:
- **Email nhóm**: [email]
- **GitHub**: [link nếu có]

---

## License & Attribution

- Dataset sử dụng theo giấy phép của Kaggle - Educational use only
- Dự án này được thực hiện cho môn CSC17104 - Programming for Data Science
- Trường Đại học Khoa học Tự nhiên, ĐHQG-HCM

---

**Ngày cập nhật**: [Ngày tháng năm]

**Trạng thái dự án**: 🚧 Đang thực hiện (In Progress)
