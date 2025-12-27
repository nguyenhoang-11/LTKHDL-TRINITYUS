# Dự Án: Phân Tích và Dự Đoán Nguy Cơ Đột Quỵ

## Thông Tin Dự Án

**Tên dự án:** Phân tích và dự đoán nguy cơ đột quỵ dựa trên dữ liệu y tế

**Môn học:** Lập trình cho Khoa học Dữ liệu (Programming for Data Science) - CSC17104

**Học kỳ:** I - Năm học 2024-2025

**Trường:** Đại học Khoa học Tự nhiên - ĐHQG TP.HCM

---

## Thông Tin Nhóm

**Mã nhóm: 02 - Trinity US**

| STT | Họ và Tên           | MSSV     | Email                         |
|-----|---------------------|----------|-------------------------------|
| 1   | Bùi Đoàn Thúy Vy    | 22120448 | 22120448@student.hcmus.edu.vn |
| 2   | Phạm Trần Trung Hậu | 22120100 | 22120100@student.hcmus.edu.vn |
| 3   | Nguyễn Việt Hoàng   | 22120113 | 22120113@student.hcmus.edu.vn |

---

## Tổng Quan Dự Án

### Mục Tiêu

Dự án này phân tích dữ liệu y tế của 5,110 bệnh nhân nhằm:
- Xác định các yếu tố nguy cơ chính liên quan đến đột quỵ
- Trả lời 6 câu hỏi nghiên cứu về mối quan hệ giữa các yếu tố với nguy cơ đột quỵ
- Xây dựng mô hình Machine Learning để dự đoán nguy cơ đột quỵ
- Rút ra các khuyến nghị có ý nghĩa cho chính sách y tế và phòng ngừa bệnh

### Bối Cảnh

Theo Tổ chức Y tế Thế giới (WHO), đột quỵ là nguyên nhân gây tử vong đứng thứ hai trên toàn cầu. Việc phát hiện sớm các yếu tố nguy cơ có ý nghĩa quan trọng trong:
- Phòng ngừa bệnh và giảm tỷ lệ tử vong
- Hỗ trợ bác sĩ trong quyết định lâm sàng
- Xây dựng hệ thống cảnh báo sớm dựa trên dữ liệu

---

## Bộ Dữ Liệu

### Thông Tin Cơ Bản

- **Tên:** Stroke Prediction Dataset
- **Nguồn:** Kaggle
- **URL:** https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset
- **Kích thước:** 5,110 bệnh nhân × 12 đặc trưng
- **Định dạng:** CSV
- **Giấy phép:** Kaggle Dataset License

### Các Đặc Trưng

**Thông tin nhân khẩu học:**
- `gender`: Giới tính (Male/Female/Other)
- `age`: Tuổi của bệnh nhân
- `ever_married`: Tình trạng hôn nhân (Yes/No)
- `work_type`: Loại hình công việc
- `Residence_type`: Nơi cư trú (Urban/Rural)

**Thông tin sức khỏe:**
- `hypertension`: Tăng huyết áp (0 = Không, 1 = Có)
- `heart_disease`: Bệnh tim (0 = Không, 1 = Có)
- `avg_glucose_level`: Mức đường huyết trung bình (mg/dL)
- `bmi`: Chỉ số khối cơ thể (kg/m²)
- `smoking_status`: Tình trạng hút thuốc

**Biến mục tiêu:**
- `stroke`: Tình trạng đột quỵ (0 = Không, 1 = Có)

---

## Các Câu Hỏi Nghiên Cứu

Dự án trả lời 6 câu hỏi nghiên cứu chính:

### Q1: Young vs Old Stroke Patterns

**Nội dung:** Trong nhóm bệnh nhân đã bị đột quỵ, người trẻ (< 40 tuổi) có chịu tác động chủ yếu từ yếu tố lối sống hay bệnh nền?

**Notebook:** `04_Q1_Young_vs_Old_Stroke_Patterns.ipynb`

**Phát hiện chính:**
- Người trẻ bị đột quỵ chủ yếu do **lối sống không lành mạnh** (hút thuốc, ít vận động, stress)
- Người già bị đột quỵ chủ yếu do **bệnh nền tích lũy** (tăng huyết áp, bệnh tim)
- Cần chiến lược phòng ngừa khác nhau cho từng nhóm tuổi

### Q2: Urban Health vs Lifestyle Paradox

**Nội dung:** Trong khu vực đô thị, trong nhóm đã bị đột quỵ, nhóm nào chiếm ưu thế:
- Sức khỏe sinh học TỐT + Lối sống XẤU?
- Hay Sức khỏe sinh học XẤU + Lối sống TỐT?

**Notebook:** `05_Q2_Urban_Health_vs_Lifestyle_Paradox.ipynb`

**Phát hiện chính:**
- **Lối sống xấu có thể "đánh bại" chỉ số sinh học tốt**
- Nhóm có BMI, glucose bình thường nhưng hút thuốc, ít vận động có nguy cơ cao hơn
- Không thể chỉ dựa vào xét nghiệm để đánh giá nguy cơ

### Q3: Smoking × Age Interaction

**Nội dung:** Có tương tác giữa hút thuốc và tuổi tác trong việc ảnh hưởng đến nguy cơ đột quỵ?

**Notebook:** `06_Q3_Smoking_Age_Interaction.ipynb`

**Phát hiện chính:**
- Ảnh hưởng của hút thuốc **KHÁC NHAU** giữa các nhóm tuổi
- Người trẻ: Hút thuốc tác động rất mạnh
- Người cao tuổi: Tuổi tác che lấp tác động của hút thuốc
- Chiến dịch cai thuốc cần tập trung vào **nhóm trẻ và trung niên**

### Q4: Glucose × Gender Interaction

**Nội dung:** Có tương tác giữa mức glucose và giới tính trong việc ảnh hưởng đến nguy cơ đột quỵ?

**Notebook:** `07_Q4_Glucose_Gender_Interaction.ipynb`

**Phát hiện chính:**
- **Nam giới nhạy cảm hơn** với glucose cao
- **Nữ giới** có thể được bảo vệ bởi hormone (estrogen)
- Cần **tiêu chuẩn khác nhau** cho nam và nữ trong kiểm soát glucose
- Nam giới cần can thiệp sớm hơn khi glucose tăng

### Q5: Urban Rural Heart Disease (Urban Penalty)

**Nội dung:** Tại sao người đô thị có bệnh tim lại có tỷ lệ đột quỵ cao hơn nông thôn, đặc biệt ở nam giới?

**Notebook:** `08_Q5_Urban_Rural_Heart_Disease.ipynb`

**Phát hiện chính:**
- **Nam đô thị có bệnh tim:** 20.5% stroke rate
- **Nam nông thôn có bệnh tim:** 13.8% stroke rate
- **Chênh lệch:** +6.7% (Urban penalty)
- **Nữ giới:** Gần như không có urban penalty (+0.2%)
- Nam giới bị ảnh hưởng ~33 lần nữ giới

**Đặc biệt:**
- Phân tích Statistical vs Clinical Significance (p > 0.05 nhưng vẫn quan trọng)
- Precautionary Principle trong y tế công cộng
- Limitations & Future Directions chi tiết

### Q6: Machine Learning - Behavioral Persona Prediction

**Nội dung:** Dự đoán đột quỵ dựa trên Behavioral Personas có tốt hơn chỉ dựa vào đặc điểm nhân khẩu học?

**Notebook:** `09_Q6_ML_Behavioral_Persona_Prediction.ipynb`

**Phương pháp:**
- Tạo 6 behavioral personas bằng K-Means clustering
- So sánh 3 models: **Logistic Regression, Random Forest, XGBoost**
- Xử lý class imbalance bằng SMOTE
- Feature Importance analysis

**Kết quả:**
- **Best model:** Random Forest (ROC-AUC = 0.6436)
- **Personas có giá trị:** Phân biệt nguy cơ lên đến 4.8 lần
- **Top features:** Age, Glucose, Hypertension, Heart disease, BMI

---

## Cấu Trúc Dự Án

```
ĐỒ ÁN CUỐI KÌ/
│
├── data/
│   ├── healthcare-dataset-stroke-data.csv    # Dữ liệu gốc
│   └── healthcare_cleaned.csv                 # Dữ liệu đã xử lý
│
├── notebooks/
│   ├── 00_Project_Overview.ipynb              # Tổng quan dự án
│   ├── 01_Data_Collection.ipynb               # Thu thập dữ liệu
│   ├── 02_EDA.ipynb                           # Khám phá dữ liệu
│   ├── 03_Data_Preprocessing.ipynb            # Tiền xử lý
│   │
│   ├── 04_Q1_Young_vs_Old_Stroke_Patterns.ipynb         # Q1
│   ├── 05_Q2_Urban_Health_vs_Lifestyle_Paradox.ipynb    # Q2
│   ├── 06_Q3_Smoking_Age_Interaction.ipynb              # Q3
│   ├── 07_Q4_Glucose_Gender_Interaction.ipynb           # Q4
│   ├── 08_Q5_Urban_Rural_Heart_Disease.ipynb            # Q5
│   ├── 09_Q6_ML_Behavioral_Persona_Prediction.ipynb     # Q6
│   │
│   └── 10_Conclusion_Summary.ipynb            # Tổng kết
│
├── outputs/                                    # Biểu đồ, kết quả
│
├── README.md                                   # File này
└── TEAM_PLAN.pdf                              # Phân công công việc
```

**Ghi chú quan trọng:**
- Các notebooks Q1-Q6 có thể chạy độc lập
- **BẮT BUỘC** chạy `03_Data_Preprocessing.ipynb` trước để tạo `healthcare_cleaned.csv`

---

## Hướng Dẫn Chạy Dự Án

### Yêu Cầu Hệ Thống

**Phần mềm:**
- Python >= 3.8
- Jupyter Notebook hoặc JupyterLab
- Khuyến nghị: Anaconda

**Thư viện Python:**

```
pandas >= 1.3.0
numpy >= 1.21.0
matplotlib >= 3.4.0
seaborn >= 0.11.0
scikit-learn >= 1.0.0
xgboost >= 1.5.0
imbalanced-learn >= 0.9.0
scipy >= 1.7.0
```

### Cài Đặt

**Sử dụng pip:**

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost imbalanced-learn scipy
```

**Sử dụng Anaconda (Khuyến nghị):**

```bash
# Tạo môi trường mới
conda create -n stroke_analysis python=3.8

# Kích hoạt
conda activate stroke_analysis

# Cài đặt
conda install pandas numpy matplotlib seaborn scikit-learn scipy
pip install xgboost imbalanced-learn
```

### Thứ Tự Chạy

1. **`01_Data_Collection.ipynb`** - Tìm hiểu dữ liệu
2. **`02_EDA.ipynb`** - Khám phá dữ liệu
3. **`03_Data_Preprocessing.ipynb`** - Tiền xử lý (BẮT BUỘC)
4. **`04-09`** - Các câu hỏi nghiên cứu (Q1-Q6)
5. **`10_Conclusion_Summary.ipynb`** - Tổng kết

**Khởi động:**

```bash
jupyter notebook
# Hoặc
jupyter lab
```

---

## Kết Quả Chính

### Yếu Tố Nguy Cơ Mạnh Nhất

**1. Tuổi tác:**
- Nhóm đột quỵ: 67.7 tuổi (trung bình)
- Nhóm không đột quỵ: 42.0 tuổi
- **Chênh lệch:** ~25 tuổi

**2. Bệnh tim:**
- Không bệnh tim: 4.2% tỷ lệ đột quỵ
- Có bệnh tim: 17.0% tỷ lệ đột quỵ
- **Tăng:** 4.0 lần nguy cơ

**3. Tăng huyết áp:**
- Không tăng HA: 4.0% tỷ lệ đột quỵ
- Có tăng HA: 13.3% tỷ lệ đột quỵ
- **Tăng:** 3.3 lần nguy cơ

### Patterns Quan Trọng

**Urban Penalty (Nam giới):**
- Nam đô thị + bệnh tim: +6.7% nguy cơ so với nông thôn
- Nữ giới: Không bị urban penalty (+0.2%)

**Health-Lifestyle Paradox:**
- Lối sống xấu đánh bại chỉ số sinh học tốt
- Cần đánh giá tổng hợp, không chỉ xét nghiệm

**Interaction Effects:**
- Smoking × Age: Tác động khác nhau theo tuổi
- Glucose × Gender: Nam nhạy cảm hơn nữ

### Mô Hình Machine Learning

**Best Model:** Random Forest
- **ROC-AUC:** 0.6436
- **3 models so sánh:** LR, RF, XGBoost
- **Personas:** 6 nhóm hành vi
- **Risk range:** 8.5% - 40.4% (chênh lệch 4.8 lần)

---

## Phân Công Công Việc

### Bùi Đoàn Thúy Vy
- **Công việc chính:** Q1, Q2
- **Hỗ trợ:** EDA, Visualization, Code review

### Phạm Trần Trung Hậu
- **Công việc chính:** Q3, Q4
- **Hỗ trợ:** Data Preprocessing, Feature Engineering

### Nguyễn Việt Hoàng
- **Công việc chính:** Q5, Q6
- **Hỗ trợ:** Machine Learning, Project Coordination
- **Đặc biệt:** Sửa lỗi Q5, thêm Statistical Explanation và Limitations

---

## Tài Liệu Tham Khảo

### Nguồn Dữ Liệu
- Kaggle - Stroke Prediction Dataset: https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset

### Tài Liệu Khoa Học
- WHO - Stroke Statistics: https://www.who.int/news-room/fact-sheets/detail/stroke
- CDC - Stroke Facts: https://www.cdc.gov/stroke/facts.htm

### Thư Viện Python
- Pandas: https://pandas.pydata.org/
- Scikit-learn: https://scikit-learn.org/
- XGBoost: https://xgboost.readthedocs.io/
- Seaborn: https://seaborn.pydata.org/

---

## Thông Tin Liên Hệ

**Nhóm: 02 - Trinity US**

**Thành viên:**
- Bùi Đoàn Thúy Vy: 22120448@student.hcmus.edu.vn
- Phạm Trần Trung Hậu: 22120100@student.hcmus.edu.vn 
- Nguyễn Việt Hoàng: 22120113@student.hcmus.edu.vn 

---

## Giấy Phép

Dự án này được thực hiện cho mục đích học tập trong khuôn khổ môn học Programming for Data Science (CSC17104) tại Đại học Khoa học Tự nhiên - ĐHQG TP.HCM.

Bộ dữ liệu sử dụng tuân theo Kaggle Dataset License và chỉ được sử dụng cho mục đích nghiên cứu và học tập.

---

## Lời Cảm Ơn

Nhóm xin chân thành cảm ơn:
- Thầy/Cô giảng viên môn Programming for Data Science
- Kaggle và tác giả fedesoriano đã cung cấp bộ dữ liệu
- Cộng đồng Python và Data Science

---

**Cập nhật lần cuối:** 27/12/2025

**Phiên bản:** 6.0
