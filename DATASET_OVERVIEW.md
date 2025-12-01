# TỔNG QUAN BỘ DỮ LIỆU STROKE PREDICTION
# STROKE PREDICTION DATASET OVERVIEW

**Dựa trên phân tích từ stroke_analysis.ipynb**

---

## 📊 1. THÔNG TIN Cơ BẢN

### Nguồn và Kích thước:
- **Nguồn:** Kaggle - Stroke Prediction Dataset
- **Kích thước:** 5,110 bệnh nhân × 12 đặc trưng
- **Mục đích:** Dự đoán nguy cơ đột quỵ dựa trên thông tin lâm sàng và nhân khẩu học

### Đáp ứng yêu cầu đồ án:
- ✅ Số hàng ≥ 1000: **5,110 records**
- ✅ Số cột ≥ 10: **12 columns**
- ✅ Không có duplicate records
- ✅ Có missing data nhẹ (~4%)

---

## 🏥 2. CẤU TRÚC DỮ LIỆU

### 2.1 Các Đặc Trưng (12 Columns)

#### **A. Thông Tin Định Danh:**
| Column | Type | Description |
|--------|------|-------------|
| `id` | int64 | ID bệnh nhân (67 - 72,940) |

#### **B. Thông Tin Nhân Khẩu Học (Demographics):**
| Column | Type | Values | Distribution |
|--------|------|--------|--------------|
| `gender` | object | Male/Female/Other | Female: 58.6%, Male: 41.4%, Other: 0.02% |
| `age` | float64 | 0.08 - 82 tuổi | Mean: 43.2, Median: 45 |
| `ever_married` | object | Yes/No | Yes: 65.6%, No: 34.4% |
| `work_type` | object | 5 loại | Private: 57.2%, Self-employed: 16%, Children: 13.4%, Govt: 12.9%, Never: 0.4% |
| `Residence_type` | object | Urban/Rural | Urban: 50.8%, Rural: 49.2% |

#### **C. Thông Tin Sức Khỏe (Health Indicators):**
| Column | Type | Range | Distribution |
|--------|------|-------|--------------|
| `hypertension` | int64 | 0/1 | Có: 9.7%, Không: 90.3% |
| `heart_disease` | int64 | 0/1 | Có: 5.4%, Không: 94.6% |
| `avg_glucose_level` | float64 | 55.1 - 271.7 mg/dL | Mean: 106.1, Median: 91.9 |
| `bmi` | float64 | 10.3 - 97.6 kg/m² | Mean: 28.9, Median: 28.1 |
| `smoking_status` | object | 4 loại | Never: 37%, Unknown: 30.2%, Formerly: 17.3%, Smokes: 15.4% |

#### **D. Biến Mục Tiêu (Target):**
| Column | Type | Distribution | Imbalance Ratio |
|--------|------|--------------|-----------------|
| `stroke` | int64 | 0: 4,861 (95.1%)<br>1: 249 (4.9%) | **1:19.5** |

---

## 🔍 3. PHÂN TÍCH DỮ LIỆU THIẾU

### Missing Data Summary:
| Column | Missing Count | Percentage | Note |
|--------|---------------|------------|------|
| `bmi` | 201 | **3.93%** | Duy nhất có missing |
| Tất cả còn lại | 0 | 0% | Complete data |

### Missing Pattern:
- **201 records** (3.93%) thiếu BMI
- Missing **KHÔNG hoàn toàn random** (MNAR):
  - Nhóm có BMI: 4.87% stroke rate
  - Nhóm thiếu BMI: Khác biệt có ý nghĩa
- **Chiến lược xử lý:** Mean/Median imputation hoặc deletion

---

## 📈 4. PHÂN BỐ BIẾN MỤC TIÊU (TARGET ANALYSIS)

### Class Imbalance - VẤN ĐỀ QUAN TRỌNG NHẤT:

```
Không đột quỵ (0): 4,861 ca (95.13%)
Đột quỵ (1):         249 ca (4.87%)
────────────────────────────────────
Tỷ lệ:              1:19.5 (severe imbalance)
```

### Ý Nghĩa:
- ✅ **Phản ánh thực tế y tế:** Tỷ lệ đột quỵ trong dân số thấp
- ⚠️ **Thách thức ML:** Accuracy misleading, cần metrics đặc biệt
- ✅ **Giải pháp:** SMOTE, ROC-AUC, Recall thay vì Accuracy

---

## 🔬 5. PHÂN TÍCH CÁC BIẾN SỐ

### 5.1 Tuổi (Age):

**Phân bố:**
- Min: 0.08 tuổi (trẻ sơ sinh)
- Mean: 43.2 tuổi
- Median: 45 tuổi
- Max: 82 tuổi
- Distribution: Tương đối uniform, có peak ở 40-60

**So sánh theo Stroke:**
| Group | Mean | Std | p-value |
|-------|------|-----|---------|
| Không stroke | 41.97 | 22.29 | |
| Có stroke | **67.73** | 12.73 | **<0.001*** |

**Insight:** Tuổi là yếu tố nguy cơ MẠNH NHẤT (chênh lệch 25.76 tuổi)

### 5.2 Glucose Level:

**Phân bố:**
- Min: 55.1 mg/dL
- Mean: 106.1 mg/dL
- Median: 91.9 mg/dL
- Max: 271.7 mg/dL

**So sánh theo Stroke:**
| Group | Mean | Std | p-value |
|-------|------|-----|---------|
| Không stroke | 104.80 | 43.85 | |
| Có stroke | **132.54** | 61.92 | **<0.001*** |

**Insight:** Glucose cao hơn rõ rệt ở nhóm stroke (+27.74 mg/dL)

### 5.3 BMI:

**Phân bố:**
- Min: 10.3 kg/m²
- Mean: 28.9 kg/m²
- Median: 28.1 kg/m²
- Max: 97.6 kg/m²

**So sánh theo Stroke:**
| Group | Mean | Std | p-value |
|-------|------|-----|---------|
| Không stroke | 28.82 | 7.91 | |
| Có stroke | 30.47 | 6.33 | **0.003** |

**Insight:** BMI có khác biệt nhưng YẾU HƠN glucose và age

---

## 🏷️ 6. PHÂN TÍCH CÁC BIẾN PHÂN LOẠI

### 6.1 Mối Liên Hệ với Stroke (Chi-square Tests):

| Variable | Chi-square | p-value | Significant? | Stroke Rate |
|----------|-----------|---------|--------------|-------------|
| **hypertension** | 81.605 | <0.001 | ✅ YES | Có: 13.25%, Không: 3.97% |
| **heart_disease** | 90.260 | <0.001 | ✅ YES | Có: 17.03%, Không: 4.18% |
| **ever_married** | 58.924 | <0.001 | ✅ YES | Yes: 6.50%, No: 1.62% |
| **work_type** | 49.164 | <0.001 | ✅ YES | Self-employed cao nhất |
| **smoking_status** | 29.147 | <0.001 | ✅ YES | Formerly smoked cao nhất |
| gender | 0.473 | 0.790 | ❌ NO | Không khác biệt |
| Residence_type | 1.082 | 0.298 | ❌ NO | Không khác biệt |

### 6.2 Chi Tiết Từng Biến:

#### **Gender (KHÔNG có ý nghĩa):**
- Female: 58.6% → Stroke rate: ~4.9%
- Male: 41.4% → Stroke rate: ~4.9%
- **Kết luận:** Không có sự khác biệt về giới tính

#### **Hypertension (Có ý nghĩa):**
- Không: 90.3% → Stroke rate: 3.97%
- Có: 9.7% → Stroke rate: **13.25%**
- **Odds Ratio:** ~3.3x nguy cơ

#### **Heart Disease (Có ý nghĩa):**
- Không: 94.6% → Stroke rate: 4.18%
- Có: 5.4% → Stroke rate: **17.03%**
- **Odds Ratio:** ~4.1x nguy cơ

#### **Marriage Status (Có ý nghĩa - confounded by age):**
- Yes: 65.6% → Stroke rate: 6.50%
- No: 34.4% → Stroke rate: 1.62%
- **Lưu ý:** Có thể do người đã kết hôn GIÀ HƠN

#### **Work Type (Có ý nghĩa):**
| Type | Count | % | Stroke Rate |
|------|-------|---|-------------|
| Self-employed | 819 | 16.0% | **~8.0%** (cao nhất) |
| Private | 2,925 | 57.2% | ~5.5% |
| Govt_job | 657 | 12.9% | ~4.5% |
| Children | 687 | 13.4% | ~0.3% (thấp nhất) |
| Never_worked | 22 | 0.4% | 0% |

#### **Smoking Status (Có ý nghĩa - SURPRISING!):**
| Status | Count | % | Stroke Rate |
|--------|-------|---|-------------|
| **Formerly smoked** | 885 | 17.3% | **7.3%** (cao nhất!) |
| Smokes | 789 | 15.4% | 5.0% |
| Never smoked | 1,892 | 37.0% | 3.7% |
| Unknown | 1,544 | 30.2% | 2.9% (thấp nhất) |

**🔥 COUNTERINTUITIVE:** Formerly smokers có nguy cơ cao hơn current smokers!

#### **Residence Type (KHÔNG có ý nghĩa):**
- Urban: 50.8% → Stroke rate: ~5.1%
- Rural: 49.2% → Stroke rate: ~4.7%
- **Kết luận:** Không có khác biệt Urban vs Rural

---

## 📊 7. CORRELATION ANALYSIS

### Ma Trận Tương Quan với Stroke:

| Feature | Correlation | Strength |
|---------|-------------|----------|
| **age** | **+0.245** | Mạnh nhất |
| **heart_disease** | +0.129 | Trung bình |
| **hypertension** | +0.128 | Trung bình |
| **avg_glucose_level** | +0.132 | Trung bình |
| **bmi** | +0.042 | Yếu |

### Insights:
- **Age** là predictor mạnh nhất (r = 0.245)
- Health indicators (heart, hypertension, glucose) tương đương nhau
- BMI có correlation YẾU NHẤT

---

## 🎯 8. PHÁT HIỆN QUAN TRỌNG TỪ Q1 & Q2

### Từ Q1 (Age, Hypertension, Heart Disease):

#### **Age Distribution theo Stroke:**
| Age Group | Total | Stroke Cases | Stroke Rate |
|-----------|-------|--------------|-------------|
| 0-20 | 1,025 | 2 | **0.20%** |
| 21-40 | 1,219 | 6 | 0.49% |
| 41-60 | 1,562 | 64 | 4.10% |
| 61-80 | 1,188 | 154 | **12.96%** |
| 81+ | 116 | 23 | **19.83%** |

**Pattern:** Tăng theo cấp số nhân! (0.2% → 4% → 13% → 20%)

#### **Interaction Effects:**
| Age + Conditions | Stroke Rate |
|------------------|-------------|
| 61-80 + Cả 2 bệnh lý (HA + Heart) | **20.93%** |
| 81+ + Cả 2 bệnh lý | **30.00%** |
| 61-80 + Không có bệnh lý | 10.31% |

**Synergistic Effect:** Có cả 2 bệnh lý tăng nguy cơ nhiều hơn TỔNG của từng yếu tố!

### Từ Q2 (Glucose, BMI):

#### **Glucose Categories:**
| Category | Range | Count | Stroke Rate |
|----------|-------|-------|-------------|
| Bình thường | <140 | 4,289 | 3.64% |
| Tiền đái tháo đường | 140-200 | 387 | 9.56% |
| Đái tháo đường | ≥200 | 434 | **12.90%** |

**Pattern:** Tăng gấp 3.5x từ normal → diabetes

#### **BMI Categories (WHO):**
| Category | Range | Count | Stroke Rate |
|----------|-------|-------|-------------|
| Thiếu cân | <18.5 | 349 | 0.29% |
| Bình thường | 18.5-25 | 1,258 | 2.94% |
| **Thừa cân** | 25-30 | 1,610 | **7.14%** (!) |
| Béo phì | ≥30 | 1,893 | 5.07% |

**🔥 SURPRISING:** Thừa cân (25-30) có nguy cơ CAO HƠN béo phì (>30)!

#### **Glucose × BMI Interaction:**
| BMI ↓ / Glucose → | Normal | Prediabetes | Diabetes |
|-------------------|--------|-------------|----------|
| Thiếu cân | 0.30% | 0% | 0% |
| Bình thường | 2.15% | 5.88% | 9.38% |
| Thừa cân | 5.33% | 13.33% | 17.86% |
| Béo phì | 3.44% | 10.17% | 12.50% |

**Pattern:** Glucose effect mạnh hơn BMI effect!

---

## ⚠️ 9. VẤN ĐỀ VÀ THÁCH THỨC

### 9.1 Class Imbalance (Quan trọng nhất):
- **Vấn đề:** 95:5 ratio
- **Hệ quả:** Accuracy misleading (có thể đạt 95% bằng cách predict all = 0)
- **Giải pháp:**
  - ✅ SMOTE cho training data
  - ✅ Metrics: ROC-AUC, Precision-Recall, F1
  - ✅ Stratified sampling
  - ❌ KHÔNG dùng Accuracy làm metric chính

### 9.2 Missing Data:
- **BMI:** 3.93% missing
- **Impact:** Nhẹ, có thể handle bằng imputation
- **Strategies:** Mean, Median, hoặc Group mean imputation

### 9.3 Confounding Factors:
- **Marriage ← Age:** Người kết hôn thường già hơn
- **Formerly smokers:** Có thể già hơn current smokers
- **Work type ← Age:** Children group rất trẻ

### 9.4 Data Quality:
- ✅ Không có duplicates
- ✅ Không có outliers cực đoan
- ⚠️ Có 1 record gender = "Other" (có thể remove)
- ⚠️ Smoking "Unknown" chiếm 30% (khá cao)

---

## 💡 10. INSIGHTS CHO NGHIÊN CỨU

### 10.1 Risk Factors Ranking:

| Rank | Factor | Evidence | Strength |
|------|--------|----------|----------|
| 🥇 1 | **Age** | r=0.245, 0.2%→20% across groups | Very Strong |
| 🥈 2 | **Heart Disease** | OR=4.1x, p<0.001 | Strong |
| 🥉 3 | **Hypertension** | OR=3.3x, p<0.001 | Strong |
| 4 | **Glucose** | +27 mg/dL, p<0.001 | Strong |
| 5 | **Smoking** | Formerly: 7.3%, p<0.001 | Medium |
| 6 | **Work type** | Self-employed: 8%, p<0.001 | Medium |
| 7 | **BMI** | +1.65, p=0.003 | Weak |
| ❌ | Gender | p=0.79 | No effect |
| ❌ | Residence | p=0.30 | No effect |

### 10.2 Surprising Findings:

1. **Formerly smokers > Current smokers** (7.3% vs 5.0%)
   - Hypothesis: Age confounding
   - Cần phân tích sâu hơn

2. **Overweight > Obese** (7.1% vs 5.1% stroke rate)
   - Counterintuitive!
   - Có thể do obesity paradox

3. **Married > Single** (6.5% vs 1.6%)
   - Rõ ràng là age confounding
   - Cần control for age

4. **Gender không có effect** (p=0.79)
   - Khác với nhiều nghiên cứu khác
   - Có thể do sample size hoặc data quality

### 10.3 Clinical Implications:

**High Risk Profile:**
- Age >60
- Has hypertension OR heart disease (better: both)
- Glucose >140
- Formerly smoked
- Self-employed (stress?)

**Priority Screening Groups:**
- Age 61-80 với ≥1 comorbidity
- Age >80 (regardless)
- Diabetes + overweight

**Modifiable Factors:**
- ✅ Glucose control (strong effect)
- ✅ Blood pressure management
- ✅ Quit smoking (long-term benefit)
- ⚠️ Weight loss (moderate effect)

---

## 📌 11. KHUYẾN NGHỊ CHO PHÂN TÍCH TIẾP THEO

### 11.1 Cần Làm Rõ:

1. **Age confounding:**
   - Stratified analysis by age groups
   - Control for age trong multivariate analysis

2. **Smoking paradox:**
   - Age distribution của formerly vs current
   - Duration since quit?

3. **BMI paradox:**
   - Phân tích glucose × BMI interaction chi tiết hơn
   - Có thể obesity paradox?

4. **Missing data impact:**
   - So sánh deletion vs imputation
   - Check if MNAR affects results

### 11.2 Câu Hỏi Nghiên Cứu Tiềm Năng:

1. ✅ Young stroke (<40): Risk factors khác gì?
2. ✅ Glucose vs BMI: Ai independent hơn?
3. ✅ Smoking timeline: Bao lâu sau quit mới safe?
4. ✅ Multi-modal ML: Expert models ensemble?
5. ✅ Cost-sensitive learning: Optimize cho Recall
6. ✅ SHAP interpretability: Individual predictions

### 11.3 Machine Learning Considerations:

**Preprocessing cần thiết:**
- [ ] Handle missing BMI (imputation)
- [ ] Encode categorical variables
- [ ] Feature scaling (StandardScaler)
- [ ] **SMOTE** cho training set (quan trọng!)
- [ ] Stratified train-test split

**Models đề xuất:**
- Logistic Regression (baseline, interpretable)
- Random Forest (handles interactions)
- XGBoost (best performance expected)
- Gradient Boosting (robust)

**Evaluation metrics:**
- ✅ ROC-AUC (primary)
- ✅ Precision-Recall curves
- ✅ Recall (critical cho medical)
- ✅ F1-Score
- ❌ KHÔNG dùng Accuracy

---

## 📝 12. TÓM TẮT EXECUTIVE

### Dataset Quality: ★★★★☆ (4/5)
- ✅ Size đủ lớn (5,110)
- ✅ Missing data thấp (3.93%)
- ✅ No duplicates
- ⚠️ Severe class imbalance (cần xử lý)
- ⚠️ Some confounding factors

### Research Potential: ★★★★★ (5/5)
- ✅ Clear target variable
- ✅ Mix of demographic + health data
- ✅ Surprising findings (paradoxes)
- ✅ Real-world medical relevance
- ✅ Multiple research angles

### Key Takeaways:

1. **Age dominates** all other factors
2. **Glucose > BMI** trong dự đoán stroke
3. **Class imbalance** là challenge chính cho ML
4. **Confounding factors** cần control carefully
5. **Surprising paradoxes** make research interesting

---

**Generated from:** stroke_analysis.ipynb (Sections 1-4.2)
**Last updated:** 2025-11-30
**Analysis depth:** Comprehensive EDA + Q1 + Q2 complete
