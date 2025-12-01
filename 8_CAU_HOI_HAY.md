# 8 CÂU HỎI NGHIÊN CỨU SÁNG TẠO
# 8 CREATIVE RESEARCH QUESTIONS

**Dựa trên Stroke Prediction Dataset - Không giới hạn bởi Q1, Q2**

---

## 🎯 TRIẾT LÝ CHỌN CÂU HỎI

### ❌ Tránh các câu hỏi:
- Quá đơn giản, mô tả (descriptive only)
- Không có actionable insights
- Kết quả dễ đoán trước
- Không liên kết với nhau

### ✅ Ưu tiên câu hỏi:
- **Surprising findings**: Kết quả bất ngờ, thách thức quan niệm
- **Actionable insights**: Có thể áp dụng thực tế
- **Story-telling**: Câu hỏi kết nối với nhau tạo thành câu chuyện
- **Medical relevance**: Có ý nghĩa lâm sàng thực sự

---

## 📊 8 CÂU HỎI ĐỀ XUẤT

---

## **Q1: The Age Paradox - Tuổi trẻ có thực sự an toàn?**

### **Câu hỏi:**
Trong nhóm < 40 tuổi, yếu tố nào là "red flag" mạnh nhất cho đột quỵ sớm? Liệu các yếu tố truyền thống (HA, tim) có cùng mức độ nguy hiểm ở người trẻ như người già?

### **Tại sao HAY:**
- ✅ **Phá vỡ stereotype**: "Đột quỵ chỉ xảy ra ở người già"
- ✅ **Early intervention**: Tìm dấu hiệu cảnh báo sớm
- ✅ **Surprising**: Có thể phát hiện patterns khác với người già

### **Phân tích:**
```python
# So sánh risk factors giữa young (<40) và old (>60) stroke patients
young_stroke = df[(df['age'] < 40) & (df['stroke'] == 1)]
old_stroke = df[(df['age'] > 60) & (df['stroke'] == 1)]

# Feature comparison: glucose, BMI, hypertension dominance
# Odds Ratio calculation for each age group
```

### **Expected Insights:**
- Glucose có thể quan trọng HƠN ở người trẻ
- Young stroke patients có profile khác biệt
- Early warning signs for 20-40 age group

### **Độ khó:** ⭐⭐⭐ | **Impact:** 🔥🔥🔥🔥🔥

---

## **Q2: The Glucose-BMI Paradox - Ai là thủ phạm thực sự?**

### **Câu hỏi:**
Khi kiểm soát glucose, liệu BMI còn có ý nghĩa? Ngược lại, khi kiểm soát BMI, glucose có còn quan trọng? Ai là yếu tố độc lập mạnh hơn?

### **Tại sao HAY:**
- ✅ **Medical debate**: Béo phì vs Đái tháo đường - ai nguy hiểm hơn?
- ✅ **Confounding analysis**: Phân tích sâu hơn mối quan hệ
- ✅ **Actionable**: Focus vào yếu tố nào trước?

### **Phân tích:**
```python
# Stratified analysis
# Group 1: Normal glucose + High BMI → stroke rate?
# Group 2: High glucose + Normal BMI → stroke rate?
# Group 3: Both high → stroke rate?
# Group 4: Both normal → stroke rate?

# Multivariate logistic regression
# Control for age, then see glucose vs BMI coefficient
```

### **Expected Insights:**
- Glucose là independent predictor mạnh hơn
- High glucose + Normal BMI nguy hiểm hơn Normal glucose + High BMI
- BMI effect biến mất khi control glucose

### **Độ khó:** ⭐⭐⭐⭐ | **Impact:** 🔥🔥🔥🔥

---

## **Q3: The Smoking Timeline - Bao lâu sau khi quit mới an toàn?**

### **Câu hỏi:**
Formerly smokers có stroke rate cao hơn current smokers (surprising!). Điều này cho thấy gì về residual risk? Liệu quit smoking có thực sự giảm nguy cơ ngay lập tức?

### **Tại sao HAY:**
- ✅ **Counterintuitive finding**: Formerly > Current (phản trực giác)
- ✅ **Timeline analysis**: Bao lâu thì an toàn?
- ✅ **Public health**: Thông điệp quan trọng cho người muốn quit

### **Phân tích:**
```python
# Deep dive into smoking_status
# Compare: Never vs Current vs Formerly vs Unknown

# Interaction with age
# Young smokers vs Old smokers vs Formerly smokers

# Hypothesis: Formerly smokers GIÀ HƠN → confounding factor
```

### **Expected Insights:**
- Formerly smokers có age cao hơn → đó mới là lý do
- Sau khi control age, quit smoking VẪN beneficial
- Message: Quit càng sớm càng tốt

### **Độ khó:** ⭐⭐⭐ | **Impact:** 🔥🔥🔥🔥

---

## **Q4: The Married Penalty - Vì sao người đã kết hôn có nguy cơ cao hơn?**

### **Câu hỏi:**
Married vs Single có stroke rate chênh lệch lớn (6.5% vs 1.6%). Đây có phải chỉ là age confounding, hay còn factors khác? Work-life balance, stress, lifestyle changes?

### **Tại sao HAY:**
- ✅ **Social determinants**: Không chỉ y tế, mà còn xã hội
- ✅ **Lifestyle changes**: Kết hôn → thay đổi gì?
- ✅ **Multi-factor interaction**: Marriage × Work × Age

### **Phân tích:**
```python
# Stratified by age groups
# Young married vs Young single
# Old married vs Old single

# Marriage × Work type interaction
# Married + Self-employed vs Single + Self-employed

# Control for age → does marriage effect disappear?
```

### **Expected Insights:**
- Marriage effect biến mất sau khi control age
- Nhưng: Married + Self-employed có high stress
- Lifestyle factors: Diet, exercise changes after marriage

### **Độ khó:** ⭐⭐⭐ | **Impact:** 🔥🔥🔥

---

## **Q5: Multi-Modal Prediction - Ensemble của Ensemble**

### **Câu hỏi:**
Thay vì train 1 model trên all features, liệu training nhiều "expert models" (mỗi model focus vào 1 aspect) rồi ensemble lại có tốt hơn? Ví dụ: Model 1 (Demographics), Model 2 (Health), Model 3 (Lifestyle) → Meta-learner.

### **Tại sao HAY:**
- ✅ **Novel approach**: Không phải standard ML pipeline
- ✅ **Interpretability**: Biết được aspect nào contribute nhiều nhất
- ✅ **Advanced**: Stacked generalization

### **Phân tích:**
```python
# Expert Model 1: Demographics (age, gender, married, work, residence)
# Expert Model 2: Health (hypertension, heart_disease, glucose, BMI)
# Expert Model 3: Lifestyle (smoking_status)

# Each expert → prediction probability
# Meta-learner: Logistic Regression on 3 probabilities

# Compare với standard single model
```

### **Expected Results:**
- Ensemble-of-experts có thể tốt hơn 1-2%
- Health expert có weight cao nhất
- Interpretable: "70% risk from health, 20% demographics, 10% lifestyle"

### **Độ khó:** ⭐⭐⭐⭐⭐ | **Impact:** 🔥🔥🔥🔥🔥

---

## **Q6: Cost-Sensitive Learning - Giảm False Negatives bằng mọi giá**

### **Câu hỏi:**
Trong y tế, False Negative (bỏ sót ca bệnh) nguy hiểm hơn False Positive (dương tính giả). Liệu custom loss function ưu tiên Recall có tạo ra model khác biệt so với standard approach? Trade-off như thế nào?

### **Tại sao HAY:**
- ✅ **Medical context**: Thực tế lâm sàng quan trọng
- ✅ **Advanced ML**: Custom loss, threshold optimization
- ✅ **Actionable**: Model cho deployment thực tế

### **Phân tích:**
```python
# Approach 1: Standard model (balanced weights)
# Approach 2: Cost-sensitive (FN cost = 10 × FP cost)
# Approach 3: Threshold tuning (optimize for Recall ≥ 0.9)

# Confusion matrix comparison
# ROC curve + optimal threshold line
# Precision-Recall curve

# Business decision: Bao nhiêu FP chấp nhận được để catch 90% strokes?
```

### **Expected Results:**
- Cost-sensitive: Recall 0.95 but Precision 0.15
- Standard: Recall 0.75, Precision 0.35
- Trade-off visualization: Recall vs Resources needed

### **Độ khó:** ⭐⭐⭐⭐ | **Impact:** 🔥🔥🔥🔥🔥

---

## **Q7: Feature Interaction Discovery - Những tương tác bất ngờ**

### **Câu hỏi:**
Có những interaction effects quan trọng mà không rõ ràng? Ví dụ: BMI chỉ nguy hiểm KHI glucose cao? Hoặc hypertension chỉ nguy hiểm ở người không hút thuốc?

### **Tại sao HAY:**
- ✅ **Hidden patterns**: Phát hiện mối quan hệ ẩn
- ✅ **Personalized medicine**: Risk khác nhau cho từng profile
- ✅ **Visualization**: 3D plots, interaction heatmaps

### **Phân tích:**
```python
# Test all 2-way interactions
# Age × Glucose, Age × BMI, Glucose × BMI, etc.

# ANOVA interaction test
# Visualization: 3D surface plots

# Find top 5 strongest interactions
# Clinical interpretation
```

### **Expected Insights:**
- Age × Glucose có interaction mạnh nhất
- BMI × Smoking: Smokers với high BMI cực kỳ nguy hiểm
- Hypertension × Heart disease: Cumulative, không chỉ additive

### **Độ khó:** ⭐⭐⭐⭐ | **Impact:** 🔥🔥🔥🔥

---

## **Q8: Interpretable AI - SHAP Values cho Clinical Decision**

### **Câu hỏi:**
Với mỗi bệnh nhân cụ thể, feature nào contribute bao nhiêu % vào prediction? Tạo "explanation report" giúp bác sĩ hiểu TẠI SAO model predict high risk.

### **Tại sao HAY:**
- ✅ **Explainable AI**: Xu hướng quan trọng nhất hiện nay
- ✅ **Clinical trust**: Bác sĩ cần hiểu logic của model
- ✅ **Personalized**: Mỗi bệnh nhân có report riêng

### **Phân tích:**
```python
# Train XGBoost (best model from Q5)
# Calculate SHAP values for all predictions

# For high-risk patients:
# "Your age (75) contributes +40% risk"
# "Your glucose (180) contributes +25% risk"
# "Your hypertension contributes +15% risk"
# "Other factors: +10%"

# Waterfall plots for individual predictions
# Summary plots for global feature importance
```

### **Deliverable:**
- **Patient Report Template**
- **Top 3 modifiable factors** for each patient
- **What-if analysis**: "If you reduce glucose to 120, risk drops 15%"

### **Độ khó:** ⭐⭐⭐⭐⭐ | **Impact:** 🔥🔥🔥🔥🔥

---

## 🎓 PHÂN LOẠI CÂU HỎI

### **Theo Độ Khó:**

| Dễ (⭐⭐-⭐⭐⭐) | Trung Bình (⭐⭐⭐-⭐⭐⭐⭐) | Khó (⭐⭐⭐⭐-⭐⭐⭐⭐⭐) |
|----------------|--------------------------|----------------------|
| Q1, Q3, Q4 | Q2, Q6, Q7 | Q5, Q8 |

### **Theo Impact:**

| High Impact (🔥🔥🔥🔥🔥) | Medium Impact (🔥🔥🔥🔥) |
|------------------------|----------------------|
| Q1, Q5, Q6, Q8 | Q2, Q3, Q7 |
| | Q4 (🔥🔥🔥) |

### **Theo Loại:**

- **Clinical Focus**: Q1, Q3, Q6
- **Methodology**: Q2, Q7
- **Advanced ML**: Q5, Q8
- **Social Factors**: Q4

---

## 🎯 KHUYẾN NGHỊ COMBINATIONS

### **Option 1: Balanced & High Impact** ⭐⭐⭐⭐⭐

```
Bạn 1 (Done): Q1 (Age Paradox), Q2 (Glucose-BMI Paradox)
Bạn 2: Q3 (Smoking Timeline), Q4 (Marriage Penalty)
Bạn 3: Q5 (Multi-Modal ML), Q6 (Cost-Sensitive)
```

**Pros:**
- Story flow: Individual factors → Social → Advanced ML
- Độ khó tăng dần
- Mỗi câu đều có surprising insights

---

### **Option 2: Advanced ML Focus** ⭐⭐⭐⭐

```
Bạn 1 (Done): Q1, Q2
Bạn 2: Q3, Q7 (Feature Interactions)
Bạn 3: Q5 (Multi-Modal), Q8 (SHAP)
```

**Pros:**
- Impressive ML techniques
- Bạn 3 làm 2 câu advanced nhất
- Publication-worthy

**Cons:**
- Khó, tốn thời gian
- Risk cao

---

### **Option 3: Clinical Practical** ⭐⭐⭐⭐⭐

```
Bạn 1 (Done): Q1, Q2
Bạn 2: Q3, Q4
Bạn 3: Q6 (Cost-Sensitive), Q8 (SHAP)
```

**Pros:**
- Focus vào clinical applicability
- Mỗi câu đều có actionable insights
- Deliverables: Patient reports, decision tools

---

### **Option 4: Research Depth** ⭐⭐⭐⭐

```
Bạn 1 (Done): Q1, Q2
Bạn 2: Q2 (deep dive), Q7 (Interactions)
Bạn 3: Q5 (Multi-Modal), Q6 (Cost-Sensitive)
```

**Note:** Q2 có thể expand thành full research với multivariate analysis

---

## 💡 ĐIỂM KHÁC BIỆT SO VỚI BẢN CŨ

### **Bản cũ (An toàn nhưng nhàm):**
- ❌ Q3: "Phân tích yếu tố xã hội" → Mô tả, dễ đoán
- ❌ Q4: "Risk score 0-12" → Công thức đơn giản
- ❌ Q6: "Missing data comparison" → Standard approach

### **Bản mới (Sáng tạo, impactful):**
- ✅ Q3: "Smoking Timeline" → Phá vỡ quan niệm, surprising
- ✅ Q4: "Marriage Penalty" → Social determinants, multi-factor
- ✅ Q6: "Cost-Sensitive Learning" → Medical context, actionable
- ✅ Q5: "Multi-Modal Ensemble" → Novel approach
- ✅ Q8: "SHAP Interpretability" → Cutting-edge AI

---

## 📊 CHECKLIST CHỌN CÂU HỎI

### Mỗi câu hỏi phải có:

- [ ] **Surprising element**: Kết quả không dễ đoán
- [ ] **Actionable insights**: Có thể apply thực tế
- [ ] **Clear hypothesis**: Test được bằng data
- [ ] **Visualizations**: ≥2 plots compelling
- [ ] **Story connection**: Liên kết với câu khác
- [ ] **Medical relevance**: Ý nghĩa lâm sàng rõ ràng

---

## 🚀 RECOMMENDED FINAL CHOICE

### **Best Combination cho Impact + Feasibility:**

```
Q1: Age Paradox (Young vs Old risk factors)
Q2: Glucose-BMI Paradox (Independent effects)
Q3: Smoking Timeline (Formerly vs Current)
Q4: Marriage Penalty (Social determinants)
Q5: Multi-Modal Ensemble (BẮT BUỘC - Advanced ML)
Q6: Cost-Sensitive Learning (Medical decision-making)
```

**Lý do:**
- ✅ Câu chuyện coherent: Individual → Social → ML → Decision
- ✅ Mỗi câu đều surprising và actionable
- ✅ Độ khó balanced
- ✅ Impressive cho grading
- ✅ Publication-worthy insights

---

## 📞 NEXT STEPS

Sau khi đọc, quyết định:

1. **Chọn Option nào?** (1, 2, 3, 4, hoặc custom)
2. **Bạn 2 chọn câu nào?** (2 trong 6 câu còn lại)
3. **Bạn 3 chọn câu nào?** (Q5 + 1 trong 5 câu còn lại)

Sau đó báo cho tôi, tôi sẽ code chi tiết! 🚀

---

*"Good research questions are not just about finding answers, but about asking questions nobody has asked before."*

*Created: 2025-11-30*
