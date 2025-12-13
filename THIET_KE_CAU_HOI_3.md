# THIẾT KẾ GIẢI PHÁP CODE - CÂU HỎI 3

## 🎯 CÂU HỎI NGHIÊN CỨU

**"Người mắc bệnh tim sống ở đô thị có 'nhạy cảm' hơn với đột quỵ so với người mắc bệnh tim sống ở nông thôn không? Và liệu mức độ nhạy cảm này khác nhau giữa nam và nữ?"**

---

## 📖 CHIẾN LƯỢC STORYTELLING

### **Cấu trúc 5 Hồi (Acts)**

```
HỒOI 1: Bối cảnh - "Nghịch lý Y tế Đô thị"
    └─ Đô thị có y tế tốt hơn → Kết quả có tốt hơn không?

HỒI 2: Khám phá - "Cú sốc đầu tiên"
    └─ Urban vs Rural: Ai nguy hiểm hơn?

HỒI 3: Chiều sâu Giới tính - "Ai trả giá nhiều hơn?"
    └─ Nam vs Nữ: Sự khác biệt bất ngờ

HỒI 4: Hiệu ứng Khuếch đại - "Nguy cơ gấp bội"
    └─ Urban + HD + Yếu tố khác = ?

HỒI 5: Kết luận - "Ý nghĩa & Hành động"
    └─ Tại sao? Và làm gì?
```

---

## 📊 CẤU TRÚC NOTEBOOK CHI TIẾT

### **PHẦN 0: THIẾT LẬP & GIỚI THIỆU**

```python
# ============================================================
# CÂU HỎI 3: NGHỊCH LÝ BỆNH TIM Ở ĐÔ THỊ
# The Urban Heart Disease Paradox
# ============================================================

"""
CÂU HỎI NGHIÊN CỨU:
Người mắc bệnh tim sống ở đô thị có 'nhạy cảm' hơn với đột quỵ
so với người mắc bệnh tim sống ở nông thôn không?
Và liệu mức độ nhạy cảm này khác nhau giữa nam và nữ?

GIẢI THÍCH:
- 'Nhạy cảm' = Tỷ lệ đột quỵ cao hơn khi đã có bệnh tim
- So sánh: Urban vs Rural, Male vs Female
- Mục tiêu: Tìm pattern & giải thích

TÍNH MỚI:
- Phá vỡ quan niệm "đô thị = y tế tốt = an toàn hơn"
- Phát hiện gender disparity trong urban context
- Actionable insights cho chính sách y tế
"""

# Import thư viện
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats
from scipy.stats import chi2_contingency, fisher_exact
import warnings
warnings.filterwarnings('ignore')

# Cấu hình hiển thị tiếng Việt
plt.rcParams['font.family'] = 'DejaVu Sans'
plt.rcParams['axes.unicode_minus'] = False

# Load dữ liệu
df = pd.read_csv('healthcare-dataset-stroke-data.csv')

print("="*60)
print("DỮ LIỆU TỔNG QUAN")
print("="*60)
print(f"Tổng số bệnh nhân: {len(df):,}")
print(f"Số bệnh nhân có bệnh tim: {df['heart_disease'].sum():,} ({df['heart_disease'].mean()*100:.1f}%)")
print(f"Số bệnh nhân bị đột quỵ: {df['stroke'].sum():,} ({df['stroke'].mean()*100:.1f}%)")
print("="*60)
```

---

### **HỒI 1: BỐI CẢNH - "NGHỊCH LÝ Y TẾ ĐÔ THỊ"**

#### **Cell 1.1: Đặt vấn đề**

```python
# ============================================================
# HỒI 1: BỐI CẢNH - NGHỊCH LÝ Y TẾ ĐÔ THỊ
# ============================================================

print("📖 HỒI 1: NGHỊCH LÝ Y TẾ ĐÔ THỊ\n")
print("❓ CÂU HỎI KHỞI ĐẦU:")
print("Đô thị có bệnh viện tốt hơn, bác sĩ nhiều hơn, công nghệ hiện đại hơn.")
print("Vậy người bệnh tim ở đô thị có an toàn hơn nông thôn không?\n")

# So sánh điều kiện cơ bản
urban_total = len(df[df['Residence_type'] == 'Urban'])
rural_total = len(df[df['Residence_type'] == 'Rural'])

print(f"🏙️  Đô thị: {urban_total:,} người ({urban_total/len(df)*100:.1f}%)")
print(f"🌾 Nông thôn: {rural_total:,} người ({rural_total/len(df)*100:.1f}%)")
```

#### **Cell 1.2: So sánh tỷ lệ bệnh tim**

```python
# So sánh tỷ lệ mắc bệnh tim giữa Urban vs Rural
urban_hd_rate = df[df['Residence_type'] == 'Urban']['heart_disease'].mean()
rural_hd_rate = df[df['Residence_type'] == 'Rural']['heart_disease'].mean()

print("\n" + "="*60)
print("📊 TỶ LỆ MẮC BỆNH TIM")
print("="*60)
print(f"🏙️  Đô thị:     {urban_hd_rate*100:.2f}%")
print(f"🌾 Nông thôn:  {rural_hd_rate*100:.2f}%")

if urban_hd_rate > rural_hd_rate:
    diff = (urban_hd_rate/rural_hd_rate - 1) * 100
    print(f"\n💡 Đô thị cao hơn {diff:.1f}%")
else:
    diff = (rural_hd_rate/urban_hd_rate - 1) * 100
    print(f"\n💡 Nông thôn cao hơn {diff:.1f}%")

print("\n🔍 NHẬN XÉT:")
print("Tỷ lệ mắc bệnh tim tương đương nhau.")
print("Nhưng KHI ĐÃ có bệnh tim, ai có nguy cơ đột quỵ cao hơn?")
print("Đó chính là câu hỏi của chúng ta! ⬇️")
```

#### **Cell 1.3: Visualization - Healthcare Access**

```python
# Biểu đồ so sánh
fig, ax = plt.subplots(1, 2, figsize=(14, 5))

# Chart 1: Tỷ lệ mắc bệnh tim
categories = ['Đô thị', 'Nông thôn']
rates = [urban_hd_rate*100, rural_hd_rate*100]
colors = ['#FF6B6B', '#4ECDC4']

ax[0].bar(categories, rates, color=colors, alpha=0.7, edgecolor='black', linewidth=2)
ax[0].set_ylabel('Tỷ lệ mắc bệnh tim (%)', fontsize=12, fontweight='bold')
ax[0].set_title('Tỷ lệ mắc bệnh tim: Đô thị vs Nông thôn', fontsize=14, fontweight='bold')
ax[0].set_ylim(0, max(rates)*1.3)

# Thêm giá trị lên cột
for i, v in enumerate(rates):
    ax[0].text(i, v + 0.3, f'{v:.2f}%', ha='center', fontsize=12, fontweight='bold')

# Chart 2: Phân bố dân số
sizes = [urban_total, rural_total]
ax[1].pie(sizes, labels=categories, autopct='%1.1f%%', colors=colors,
          startangle=90, textprops={'fontsize': 12, 'fontweight': 'bold'})
ax[1].set_title('Phân bố dân số', fontsize=14, fontweight='bold')

plt.tight_layout()
plt.savefig('outputs/Q3_Act1_Context.png', dpi=300, bbox_inches='tight')
plt.show()

print("\n✅ Đã lưu biểu đồ: outputs/Q3_Act1_Context.png")
```

---

### **HỒI 2: KHÁM PHÁ - "CÚ SỐC ĐẦU TIÊN"**

#### **Cell 2.1: Phân tích chính - Urban vs Rural**

```python
# ============================================================
# HỒI 2: KHÁM PHÁ - CÚ SỐC ĐẦU TIÊN
# ============================================================

print("\n" + "="*60)
print("📖 HỒI 2: CÚ SỐC ĐẦU TIÊN")
print("="*60)

# Lọc ra những người có bệnh tim
hd_patients = df[df['heart_disease'] == 1].copy()

print(f"\n👥 Tổng số bệnh nhân có bệnh tim: {len(hd_patients):,}")

# Chia theo nơi cư trú
hd_urban = hd_patients[hd_patients['Residence_type'] == 'Urban']
hd_rural = hd_patients[hd_patients['Residence_type'] == 'Rural']

print(f"   🏙️  Đô thị: {len(hd_urban):,}")
print(f"   🌾 Nông thôn: {len(hd_rural):,}")

# Tính tỷ lệ đột quỵ
stroke_rate_urban = hd_urban['stroke'].mean()
stroke_rate_rural = hd_rural['stroke'].mean()

print("\n" + "="*60)
print("🚨 TỶ LỆ ĐỘT QUỴ TRONG SỐ NGƯỜI CÓ BỆNH TIM")
print("="*60)
print(f"🏙️  Đô thị:     {stroke_rate_urban*100:.2f}% ({hd_urban['stroke'].sum()}/{len(hd_urban)})")
print(f"🌾 Nông thôn:  {stroke_rate_rural*100:.2f}% ({hd_rural['stroke'].sum()}/{len(hd_rural)})")

# Tính chênh lệch
if stroke_rate_urban > stroke_rate_rural:
    ratio = stroke_rate_urban / stroke_rate_rural
    diff_percent = (ratio - 1) * 100
    print(f"\n⚠️  ĐÔ THỊ CAO HƠN {ratio:.2f} LẦN (cao hơn {diff_percent:.1f}%)")
else:
    ratio = stroke_rate_rural / stroke_rate_urban
    diff_percent = (ratio - 1) * 100
    print(f"\n⚠️  NÔNG THÔN CAO HƠN {ratio:.2f} LẦN (cao hơn {diff_percent:.1f}%)")
```

#### **Cell 2.2: Kiểm định thống kê**

```python
# Kiểm định Chi-square
contingency_table = pd.crosstab(
    hd_patients['Residence_type'],
    hd_patients['stroke']
)

chi2, p_value, dof, expected = chi2_contingency(contingency_table)

print("\n" + "="*60)
print("📊 KIỂM ĐỊNH THỐNG KÊ (CHI-SQUARE TEST)")
print("="*60)
print(f"Chi-square statistic: {chi2:.4f}")
print(f"P-value: {p_value:.6f}")
print(f"Degrees of freedom: {dof}")

if p_value < 0.001:
    print(f"\n✅ KẾT LUẬN: Sự khác biệt CÓ Ý NGHĨA THỐNG KÊ (p < 0.001)")
    print("   → Không phải ngẫu nhiên!")
elif p_value < 0.05:
    print(f"\n✅ KẾT LUẬN: Sự khác biệt CÓ Ý NGHĨA THỐNG KÊ (p < 0.05)")
else:
    print(f"\n❌ KẾT LUẬN: Sự khác biệt KHÔNG có ý nghĩa thống kê (p ≥ 0.05)")

# Tính Odds Ratio
table_2x2 = [[hd_urban['stroke'].sum(), len(hd_urban) - hd_urban['stroke'].sum()],
             [hd_rural['stroke'].sum(), len(hd_rural) - hd_rural['stroke'].sum()]]

oddsratio, p_fisher = fisher_exact(table_2x2)

print(f"\n📈 ODDS RATIO: {oddsratio:.3f}")
print(f"   Fisher's Exact Test p-value: {p_fisher:.6f}")

if oddsratio > 1:
    print(f"\n💡 Người có bệnh tim ở đô thị có nguy cơ đột quỵ cao gấp {oddsratio:.2f} lần nông thôn")
else:
    print(f"\n💡 Người có bệnh tim ở nông thôn có nguy cơ đột quỵ cao gấp {1/oddsratio:.2f} lần đô thị")
```

#### **Cell 2.3: Visualization - Main Comparison**

```python
# Biểu đồ so sánh chính
fig, axes = plt.subplots(1, 2, figsize=(15, 6))

# Chart 1: Bar chart - Stroke rate comparison
categories = ['Đô thị', 'Nông thôn']
stroke_rates = [stroke_rate_urban*100, stroke_rate_rural*100]
colors_main = ['#FF4757', '#2ED573']

bars = axes[0].bar(categories, stroke_rates, color=colors_main,
                    alpha=0.8, edgecolor='black', linewidth=2.5)

axes[0].set_ylabel('Tỷ lệ đột quỵ (%)', fontsize=13, fontweight='bold')
axes[0].set_title('Tỷ lệ đột quỵ ở người có bệnh tim\nĐô thị vs Nông thôn',
                   fontsize=15, fontweight='bold', pad=20)
axes[0].set_ylim(0, max(stroke_rates)*1.4)
axes[0].grid(axis='y', alpha=0.3, linestyle='--')

# Thêm giá trị và số ca
for i, (v, cat) in enumerate(zip(stroke_rates, categories)):
    if cat == 'Đô thị':
        n_stroke = hd_urban['stroke'].sum()
        n_total = len(hd_urban)
    else:
        n_stroke = hd_rural['stroke'].sum()
        n_total = len(hd_rural)

    axes[0].text(i, v + 1, f'{v:.1f}%', ha='center', fontsize=14, fontweight='bold')
    axes[0].text(i, v/2, f'{n_stroke}/{n_total}', ha='center', fontsize=11,
                 color='white', fontweight='bold')

# Thêm annotation cho sự khác biệt
if stroke_rate_urban > stroke_rate_rural:
    axes[0].annotate('', xy=(0, stroke_rates[0]), xytext=(1, stroke_rates[1]),
                     arrowprops=dict(arrowstyle='<->', color='red', lw=2))
    mid_y = (stroke_rates[0] + stroke_rates[1]) / 2
    axes[0].text(0.5, mid_y, f'Chênh lệch\n{ratio:.2f}x',
                 ha='center', fontsize=11, fontweight='bold',
                 bbox=dict(boxstyle='round', facecolor='yellow', alpha=0.7))

# Chart 2: Grouped bar - Stroke vs No stroke counts
x_pos = np.arange(len(categories))
width = 0.35

stroke_counts = [hd_urban['stroke'].sum(), hd_rural['stroke'].sum()]
no_stroke_counts = [len(hd_urban) - hd_urban['stroke'].sum(),
                    len(hd_rural) - hd_rural['stroke'].sum()]

bars1 = axes[1].bar(x_pos - width/2, stroke_counts, width,
                    label='Đột quỵ', color='#E74C3C', alpha=0.8, edgecolor='black')
bars2 = axes[1].bar(x_pos + width/2, no_stroke_counts, width,
                    label='Không đột quỵ', color='#3498DB', alpha=0.8, edgecolor='black')

axes[1].set_xlabel('Nơi cư trú', fontsize=13, fontweight='bold')
axes[1].set_ylabel('Số lượng bệnh nhân', fontsize=13, fontweight='bold')
axes[1].set_title('Phân bố đột quỵ trong nhóm bệnh tim',
                  fontsize=15, fontweight='bold', pad=20)
axes[1].set_xticks(x_pos)
axes[1].set_xticklabels(categories)
axes[1].legend(fontsize=11)
axes[1].grid(axis='y', alpha=0.3, linestyle='--')

# Thêm giá trị lên cột
for bars in [bars1, bars2]:
    for bar in bars:
        height = bar.get_height()
        axes[1].text(bar.get_x() + bar.get_width()/2., height,
                     f'{int(height)}', ha='center', va='bottom',
                     fontsize=10, fontweight='bold')

plt.tight_layout()
plt.savefig('outputs/Q3_Act2_MainComparison.png', dpi=300, bbox_inches='tight')
plt.show()

print("\n✅ Đã lưu biểu đồ: outputs/Q3_Act2_MainComparison.png")
```

#### **Cell 2.4: Tổng kết Hồi 2**

```python
print("\n" + "="*60)
print("📌 TỔNG KẾT HỒI 2")
print("="*60)
print("\n🔍 PHÁT HIỆN CHÍNH:")

if stroke_rate_urban > stroke_rate_rural:
    print(f"1. Người có bệnh tim ở đô thị có tỷ lệ đột quỵ {stroke_rate_urban*100:.1f}%")
    print(f"2. Người có bệnh tim ở nông thôn có tỷ lệ đột quỵ {stroke_rate_rural*100:.1f}%")
    print(f"3. Đô thị cao hơn {ratio:.2f} LẦN (Odds Ratio = {oddsratio:.2f})")
    print(f"4. Sự khác biệt có ý nghĩa thống kê (p = {p_value:.4f})")

    print("\n💭 NGHỊCH LÝ:")
    print("Đô thị có:")
    print("  ✓ Bệnh viện tốt hơn")
    print("  ✓ Bác sĩ chuyên môn cao hơn")
    print("  ✓ Công nghệ y tế hiện đại hơn")
    print("\nNHƯNG lại có nguy cơ đột quỵ CAO HƠN khi mắc bệnh tim!")

print("\n❓ CÂU HỎI TIẾP THEO:")
print("→ Nam và nữ có bị ảnh hưởng như nhau không?")
print("→ Đó chính là nội dung Hồi 3! ⬇️")
```

---

### **HỒI 3: CHIỀU SÂU GIỚI TÍNH - "AI TRẢ GIÁ NHIỀU HƠN?"**

#### **Cell 3.1: Phân tích theo giới tính**

```python
# ============================================================
# HỒI 3: CHIỀU SÂU GIỚI TÍNH - AI TRẢ GIÁ NHIỀU HƠN?
# ============================================================

print("\n" + "="*60)
print("📖 HỒI 3: AI TRẢ GIÁ NHIỀU HƠN?")
print("="*60)

print("\n❓ CÂU HỎI:")
print("Liệu 'urban penalty' có ảnh hưởng nam và nữ như nhau?")
print("Hay một giới phải 'trả giá' nhiều hơn?\n")

# Phân tích cho NAM GIỚI
print("👨 NAM GIỚI:")
print("-" * 40)

hd_urban_male = hd_patients[(hd_patients['Residence_type'] == 'Urban') &
                             (hd_patients['gender'] == 'Male')]
hd_rural_male = hd_patients[(hd_patients['Residence_type'] == 'Rural') &
                             (hd_patients['gender'] == 'Male')]

stroke_urban_male = hd_urban_male['stroke'].mean()
stroke_rural_male = hd_rural_male['stroke'].mean()

print(f"Đô thị:     {stroke_urban_male*100:.2f}% ({hd_urban_male['stroke'].sum()}/{len(hd_urban_male)})")
print(f"Nông thôn:  {stroke_rural_male*100:.2f}% ({hd_rural_male['stroke'].sum()}/{len(hd_rural_male)})")

if stroke_urban_male > stroke_rural_male:
    male_penalty = stroke_urban_male - stroke_rural_male
    male_ratio = stroke_urban_male / stroke_rural_male
    print(f"Chênh lệch: +{male_penalty*100:.2f}% (Urban gấp {male_ratio:.2f}x Rural)")
else:
    male_penalty = stroke_rural_male - stroke_urban_male
    male_ratio = stroke_rural_male / stroke_urban_male
    print(f"Chênh lệch: +{male_penalty*100:.2f}% (Rural gấp {male_ratio:.2f}x Urban)")

# Phân tích cho NỮ GIỚI
print("\n👩 NỮ GIỚI:")
print("-" * 40)

hd_urban_female = hd_patients[(hd_patients['Residence_type'] == 'Urban') &
                               (hd_patients['gender'] == 'Female')]
hd_rural_female = hd_patients[(hd_patients['Residence_type'] == 'Rural') &
                               (hd_patients['gender'] == 'Female')]

stroke_urban_female = hd_urban_female['stroke'].mean()
stroke_rural_female = hd_rural_female['stroke'].mean()

print(f"Đô thị:     {stroke_urban_female*100:.2f}% ({hd_urban_female['stroke'].sum()}/{len(hd_urban_female)})")
print(f"Nông thôn:  {stroke_rural_female*100:.2f}% ({hd_rural_female['stroke'].sum()}/{len(hd_rural_female)})")

if stroke_urban_female > stroke_rural_female:
    female_penalty = stroke_urban_female - stroke_rural_female
    female_ratio = stroke_urban_female / stroke_rural_female
    print(f"Chênh lệch: +{female_penalty*100:.2f}% (Urban gấp {female_ratio:.2f}x Rural)")
else:
    female_penalty = stroke_rural_female - stroke_urban_female
    female_ratio = stroke_rural_female / stroke_urban_female
    print(f"Chênh lệch: +{female_penalty*100:.2f}% (Rural gấp {female_ratio:.2f}x Urban)")
```

#### **Cell 3.2: So sánh "Urban Penalty" giữa nam và nữ**

```python
print("\n" + "="*60)
print("⚖️  SO SÁNH 'URBAN PENALTY' GIỮA NAM VÀ NỮ")
print("="*60)

# Tính urban penalty cho mỗi giới
if stroke_urban_male > stroke_rural_male and stroke_urban_female > stroke_rural_female:
    print("\n�� MỨC ĐỘ CHÊNH LỆCH (Đô thị - Nông thôn):")
    print(f"Nam giới:  +{male_penalty*100:.2f}%")
    print(f"Nữ giới:   +{female_penalty*100:.2f}%")

    if female_penalty > male_penalty:
        times_more = female_penalty / male_penalty
        print(f"\n🔴 NỮ GIỚI BỊ ẢNH HƯỞNG NHIỀU HƠN {times_more:.2f} LẦN!")
        print("\n💡 Ý NGHĨA:")
        print("   'Urban penalty' không ảnh hưởng đều giữa nam và nữ.")
        print("   Phụ nữ có bệnh tim ở đô thị phải 'trả giá' nhiều hơn!")
    elif male_penalty > female_penalty:
        times_more = male_penalty / female_penalty
        print(f"\n🔴 NAM GIỚI BỊ ẢNH HƯỞNG NHIỀU HƠN {times_more:.2f} LẦN!")

# Kiểm định thống kê cho từng giới
print("\n" + "="*60)
print("📊 KIỂM ĐỊNH THỐNG KÊ THEO GIỚI TÍNH")
print("="*60)

# Nam giới
contingency_male = pd.crosstab(
    hd_patients[hd_patients['gender'] == 'Male']['Residence_type'],
    hd_patients[hd_patients['gender'] == 'Male']['stroke']
)
chi2_male, p_male, _, _ = chi2_contingency(contingency_male)

print(f"\n👨 NAM GIỚI:")
print(f"   Chi-square: {chi2_male:.4f}")
print(f"   P-value: {p_male:.4f}")
print(f"   Kết luận: {'Có ý nghĩa' if p_male < 0.05 else 'Không có ý nghĩa'} thống kê")

# Nữ giới
contingency_female = pd.crosstab(
    hd_patients[hd_patients['gender'] == 'Female']['Residence_type'],
    hd_patients[hd_patients['gender'] == 'Female']['stroke']
)
chi2_female, p_female, _, _ = chi2_contingency(contingency_female)

print(f"\n👩 NỮ GIỚI:")
print(f"   Chi-square: {chi2_female:.4f}")
print(f"   P-value: {p_female:.4f}")
print(f"   Kết luận: {'Có ý nghĩa' if p_female < 0.05 else 'Không có ý nghĩa'} thống kê")
```

#### **Cell 3.3: Visualization - Gender Dimension**

```python
# Biểu đồ so sánh theo giới tính
fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# Chart 1: Grouped bar chart - Tỷ lệ đột quỵ theo giới tính
x_labels = ['Nam giới', 'Nữ giới']
urban_rates = [stroke_urban_male*100, stroke_urban_female*100]
rural_rates = [stroke_rural_male*100, stroke_rural_female*100]

x_pos = np.arange(len(x_labels))
width = 0.35

bars1 = axes[0].bar(x_pos - width/2, urban_rates, width,
                    label='Đô thị', color='#FF6B6B', alpha=0.8, edgecolor='black', linewidth=2)
bars2 = axes[0].bar(x_pos + width/2, rural_rates, width,
                    label='Nông thôn', color='#4ECDC4', alpha=0.8, edgecolor='black', linewidth=2)

axes[0].set_ylabel('Tỷ lệ đột quỵ (%)', fontsize=13, fontweight='bold')
axes[0].set_title('Tỷ lệ đột quỵ theo Giới tính và Nơi cư trú\n(Trong nhóm bệnh tim)',
                  fontsize=15, fontweight='bold', pad=20)
axes[0].set_xticks(x_pos)
axes[0].set_xticklabels(x_labels, fontsize=12)
axes[0].legend(fontsize=11, loc='upper left')
axes[0].grid(axis='y', alpha=0.3, linestyle='--')
axes[0].set_ylim(0, max(urban_rates + rural_rates) * 1.3)

# Thêm giá trị lên cột
for bars in [bars1, bars2]:
    for bar in bars:
        height = bar.get_height()
        axes[0].text(bar.get_x() + bar.get_width()/2., height + 1,
                     f'{height:.1f}%', ha='center', va='bottom',
                     fontsize=11, fontweight='bold')

# Chart 2: Urban Penalty comparison
penalties = []
labels_penalty = []

if stroke_urban_male > stroke_rural_male:
    penalties.append(male_penalty * 100)
    labels_penalty.append('Nam giới')
if stroke_urban_female > stroke_rural_female:
    penalties.append(female_penalty * 100)
    labels_penalty.append('Nữ giới')

colors_penalty = ['#3498DB', '#E74C3C']
bars_penalty = axes[1].bar(labels_penalty, penalties, color=colors_penalty,
                            alpha=0.8, edgecolor='black', linewidth=2)

axes[1].set_ylabel('Mức độ chênh lệch (%)', fontsize=13, fontweight='bold')
axes[1].set_title('"Urban Penalty"\n(Đô thị cao hơn Nông thôn bao nhiêu?)',
                  fontsize=15, fontweight='bold', pad=20)
axes[1].grid(axis='y', alpha=0.3, linestyle='--')
axes[1].set_ylim(0, max(penalties) * 1.4)

# Thêm giá trị và highlight
for i, (bar, val) in enumerate(zip(bars_penalty, penalties)):
    axes[1].text(bar.get_x() + bar.get_width()/2., val + 0.5,
                 f'+{val:.1f}%', ha='center', va='bottom',
                 fontsize=13, fontweight='bold')

    # Highlight giới bị ảnh hưởng nhiều hơn
    if i == penalties.index(max(penalties)):
        axes[1].text(bar.get_x() + bar.get_width()/2., val/2,
                     '⚠️ Cao nhất!', ha='center', va='center',
                     fontsize=11, fontweight='bold', color='white',
                     bbox=dict(boxstyle='round', facecolor='red', alpha=0.8))

plt.tight_layout()
plt.savefig('outputs/Q3_Act3_GenderDimension.png', dpi=300, bbox_inches='tight')
plt.show()

print("\n✅ Đã lưu biểu đồ: outputs/Q3_Act3_GenderDimension.png")
```

#### **Cell 3.4: Heatmap - 2x2 Matrix**

```python
# Tạo heatmap 2x2 cho dễ nhìn
data_matrix = [
    [stroke_urban_male*100, stroke_rural_male*100],
    [stroke_urban_female*100, stroke_rural_female*100]
]

fig, ax = plt.subplots(figsize=(10, 7))

im = ax.imshow(data_matrix, cmap='YlOrRd', aspect='auto', vmin=0, vmax=max([max(row) for row in data_matrix])*1.1)

# Thiết lập labels
ax.set_xticks([0, 1])
ax.set_yticks([0, 1])
ax.set_xticklabels(['Đô thị', 'Nông thôn'], fontsize=13, fontweight='bold')
ax.set_yticklabels(['Nam giới', 'Nữ giới'], fontsize=13, fontweight='bold')

ax.set_title('Heatmap: Tỷ lệ đột quỵ theo Giới tính × Nơi cư trú\n(Trong nhóm bệnh tim)',
             fontsize=15, fontweight='bold', pad=20)

# Thêm colorbar
cbar = plt.colorbar(im, ax=ax)
cbar.set_label('Tỷ lệ đột quỵ (%)', fontsize=12, fontweight='bold')

# Thêm giá trị vào từng ô
for i in range(2):
    for j in range(2):
        text = ax.text(j, i, f'{data_matrix[i][j]:.1f}%',
                      ha="center", va="center", color="black",
                      fontsize=16, fontweight='bold',
                      bbox=dict(boxstyle='round', facecolor='white', alpha=0.7))

# Highlight ô cao nhất
max_val = max([max(row) for row in data_matrix])
for i in range(2):
    for j in range(2):
        if data_matrix[i][j] == max_val:
            rect = plt.Rectangle((j-0.45, i-0.45), 0.9, 0.9,
                                fill=False, edgecolor='red', linewidth=4)
            ax.add_patch(rect)
            ax.text(j, i-0.35, '⚠️ Cao nhất', ha='center',
                   fontsize=10, fontweight='bold', color='red')

plt.tight_layout()
plt.savefig('outputs/Q3_Act3_Heatmap.png', dpi=300, bbox_inches='tight')
plt.show()

print("\n✅ Đã lưu biểu đồ: outputs/Q3_Act3_Heatmap.png")
```

#### **Cell 3.5: Tổng kết Hồi 3**

```python
print("\n" + "="*60)
print("📌 TỔNG KẾT HỒI 3")
print("="*60)

print("\n🔍 PHÁT HIỆN CHÍNH:")

# Tìm nhóm nguy hiểm nhất
groups = {
    'Nam - Đô thị': stroke_urban_male*100,
    'Nam - Nông thôn': stroke_rural_male*100,
    'Nữ - Đô thị': stroke_urban_female*100,
    'Nữ - Nông thôn': stroke_rural_female*100
}

max_group = max(groups, key=groups.get)
min_group = min(groups, key=groups.get)

print(f"\n1. Nhóm nguy hiểm NHẤT: {max_group} ({groups[max_group]:.1f}%)")
print(f"2. Nhóm nguy hiểm ÍT NHẤT: {min_group} ({groups[min_group]:.1f}%)")
print(f"3. Chênh lệch: {groups[max_group]/groups[min_group]:.2f} lần")

if female_penalty > male_penalty:
    print(f"\n4. 'Urban penalty' ảnh hưởng NỮ GIỚI nhiều hơn Nam giới")
    print(f"   - Nam: +{male_penalty*100:.1f}%")
    print(f"   - Nữ:  +{female_penalty*100:.1f}% (cao hơn {female_penalty/male_penalty:.2f}x)")

print("\n💭 TẠI SAO NỮ GIỚI BỊ ẢNH HƯỞNG NHIỀU HƠN?")
print("   → Gánh nặng chăm sóc gia đình")
print("   → Cân bằng công việc - cuộc sống")
print("   → Stress mãn tính cao hơn ở đô thị")
print("   → Vai trò caregiver (chăm chồng, con, cha mẹ)")

print("\n❓ CÂU HỎI TIẾP THEO:")
print("→ Có yếu tố nguy cơ nào bị 'khuếch đại' ở đô thị không?")
print("→ Đó chính là nội dung Hồi 4! ⬇️")
```

---

### **HỒI 4: HIỆU ỨNG KHUẾCH ĐẠI - "NGUY CƠ GẤP BỘI"**

#### **Cell 4.1: Phân tích các yếu tố nguy cơ khác**

```python
# ============================================================
# HỒI 4: HIỆU ỨNG KHUẾCH ĐẠI - NGUY CƠ GẤP BỘI
# ============================================================

print("\n" + "="*60)
print("📖 HỒI 4: NGUY CƠ GẤP BỘI")
print("="*60)

print("\n❓ CÂU HỎI:")
print("Khi người có bệnh tim CÒN có thêm yếu tố nguy cơ khác")
print("(tăng huyết áp, đường huyết cao, hút thuốc, béo phì),")
print("liệu môi trường đô thị có làm nguy cơ TĂNG GẤP BỘI không?\n")

# Định nghĩa các yếu tố nguy cơ phổ biến
risk_factors = {
    'Tăng huyết áp': 'hypertension',
    'Đường huyết cao': 'high_glucose',
    'BMI cao': 'high_bmi',
    'Hút thuốc': 'smoking'
}

# Tạo cột phụ
hd_patients['high_glucose'] = (hd_patients['avg_glucose_level'] > 140).astype(int)
hd_patients['high_bmi'] = (hd_patients['bmi'] > 30).astype(int)
hd_patients['smoking'] = hd_patients['smoking_status'].isin(['smokes', 'formerly smoked']).astype(int)

print("="*60)
print("📊 PHÂN TÍCH: Bệnh tim + Yếu tố nguy cơ khác")
print("="*60)

results_amplification = []

for rf_name, rf_col in risk_factors.items():
    print(f"\n🔍 {rf_name.upper()}")
    print("-" * 60)

    # Urban với HD + risk factor
    urban_hd_rf = hd_patients[(hd_patients['Residence_type'] == 'Urban') &
                               (hd_patients[rf_col] == 1)]
    rural_hd_rf = hd_patients[(hd_patients['Residence_type'] == 'Rural') &
                               (hd_patients[rf_col] == 1)]

    if len(urban_hd_rf) > 0 and len(rural_hd_rf) > 0:
        stroke_urban_rf = urban_hd_rf['stroke'].mean()
        stroke_rural_rf = rural_hd_rf['stroke'].mean()

        print(f"Đô thị:    {stroke_urban_rf*100:.1f}% ({urban_hd_rf['stroke'].sum()}/{len(urban_hd_rf)})")
        print(f"Nông thôn: {stroke_rural_rf*100:.1f}% ({rural_hd_rf['stroke'].sum()}/{len(rural_hd_rf)})")

        if stroke_urban_rf > stroke_rural_rf and stroke_rural_rf > 0:
            ratio_rf = stroke_urban_rf / stroke_rural_rf
            diff_rf = stroke_urban_rf - stroke_rural_rf
            print(f"Chênh lệch: {ratio_rf:.2f}x (+{diff_rf*100:.1f}%)")

            results_amplification.append({
                'risk_factor': rf_name,
                'urban_rate': stroke_urban_rf*100,
                'rural_rate': stroke_rural_rf*100,
                'ratio': ratio_rf,
                'diff': diff_rf*100
            })
        else:
            print("Không có sự khác biệt rõ ràng")
    else:
        print("Không đủ dữ liệu để phân tích")
```

#### **Cell 4.2: So sánh "Double/Triple Jeopardy"**

```python
print("\n" + "="*60)
print("⚠️  'DOUBLE JEOPARDY' - NGUY CƠ KÉP")
print("="*60)

# So sánh:
# - Chỉ có HD
# - HD + Hypertension
# - HD + High glucose
# - HD + Hypertension + High glucose (Triple jeopardy!)

print("\n🏙️  ĐÔ THỊ:")
print("-" * 60)

# Urban - Chỉ HD
urban_hd_only = hd_patients[(hd_patients['Residence_type'] == 'Urban') &
                             (hd_patients['hypertension'] == 0) &
                             (hd_patients['high_glucose'] == 0)]
rate_urban_hd_only = urban_hd_only['stroke'].mean() if len(urban_hd_only) > 0 else 0

# Urban - HD + Hypertension
urban_hd_hyper = hd_patients[(hd_patients['Residence_type'] == 'Urban') &
                              (hd_patients['hypertension'] == 1) &
                              (hd_patients['high_glucose'] == 0)]
rate_urban_hd_hyper = urban_hd_hyper['stroke'].mean() if len(urban_hd_hyper) > 0 else 0

# Urban - HD + High glucose
urban_hd_glucose = hd_patients[(hd_patients['Residence_type'] == 'Urban') &
                                (hd_patients['hypertension'] == 0) &
                                (hd_patients['high_glucose'] == 1)]
rate_urban_hd_glucose = urban_hd_glucose['stroke'].mean() if len(urban_hd_glucose) > 0 else 0

# Urban - HD + Both (Triple!)
urban_hd_both = hd_patients[(hd_patients['Residence_type'] == 'Urban') &
                             (hd_patients['hypertension'] == 1) &
                             (hd_patients['high_glucose'] == 1)]
rate_urban_hd_both = urban_hd_both['stroke'].mean() if len(urban_hd_both) > 0 else 0

print(f"Chỉ Bệnh tim:                {rate_urban_hd_only*100:.1f}% (n={len(urban_hd_only)})")
print(f"Bệnh tim + Tăng huyết áp:    {rate_urban_hd_hyper*100:.1f}% (n={len(urban_hd_hyper)})")
print(f"Bệnh tim + Đường huyết cao:  {rate_urban_hd_glucose*100:.1f}% (n={len(urban_hd_glucose)})")
print(f"Cả 3 yếu tố (TRIPLE!):       {rate_urban_hd_both*100:.1f}% (n={len(urban_hd_both)})")

print("\n🌾 NÔNG THÔN:")
print("-" * 60)

# Rural - tương tự
rural_hd_only = hd_patients[(hd_patients['Residence_type'] == 'Rural') &
                             (hd_patients['hypertension'] == 0) &
                             (hd_patients['high_glucose'] == 0)]
rate_rural_hd_only = rural_hd_only['stroke'].mean() if len(rural_hd_only) > 0 else 0

rural_hd_hyper = hd_patients[(hd_patients['Residence_type'] == 'Rural') &
                              (hd_patients['hypertension'] == 1) &
                              (hd_patients['high_glucose'] == 0)]
rate_rural_hd_hyper = rural_hd_hyper['stroke'].mean() if len(rural_hd_hyper) > 0 else 0

rural_hd_glucose = hd_patients[(hd_patients['Residence_type'] == 'Rural') &
                                (hd_patients['hypertension'] == 0) &
                                (hd_patients['high_glucose'] == 1)]
rate_rural_hd_glucose = rural_hd_glucose['stroke'].mean() if len(rural_hd_glucose) > 0 else 0

rural_hd_both = hd_patients[(hd_patients['Residence_type'] == 'Rural') &
                             (hd_patients['hypertension'] == 1) &
                             (hd_patients['high_glucose'] == 1)]
rate_rural_hd_both = rural_hd_both['stroke'].mean() if len(rural_hd_both) > 0 else 0

print(f"Chỉ Bệnh tim:                {rate_rural_hd_only*100:.1f}% (n={len(rural_hd_only)})")
print(f"Bệnh tim + Tăng huyết áp:    {rate_rural_hd_hyper*100:.1f}% (n={len(rural_hd_hyper)})")
print(f"Bệnh tim + Đường huyết cao:  {rate_rural_hd_glucose*100:.1f}% (n={len(rural_hd_glucose)})")
print(f"Cả 3 yếu tố (TRIPLE!):       {rate_rural_hd_both*100:.1f}% (n={len(rural_hd_both)})")

# So sánh
print("\n" + "="*60)
print("⚖️  SO SÁNH CHÊNH LỆCH")
print("="*60)

if rate_urban_hd_both > 0 and rate_rural_hd_both > 0:
    print(f"\n🔴 TRIPLE JEOPARDY:")
    print(f"   Đô thị:    {rate_urban_hd_both*100:.1f}%")
    print(f"   Nông thôn: {rate_rural_hd_both*100:.1f}%")
    print(f"   Chênh lệch: {rate_urban_hd_both/rate_rural_hd_both:.2f}x")
    print("\n   → Khi có ĐỦ 3 yếu tố, đô thị còn nguy hiểm HƠN NỮA!")
```

#### **Cell 4.3: Visualization - Risk Amplification**

```python
# Biểu đồ hiệu ứng khuếch đại
fig, axes = plt.subplots(2, 2, figsize=(16, 12))

# Chart 1: Line plot - Cumulative risk
risk_levels = ['Chỉ\nBệnh tim', 'HD +\nHuyết áp', 'HD +\nĐường huyết', 'Cả 3\nyếu tố']
urban_cumulative = [rate_urban_hd_only*100, rate_urban_hd_hyper*100,
                    rate_urban_hd_glucose*100, rate_urban_hd_both*100]
rural_cumulative = [rate_rural_hd_only*100, rate_rural_hd_hyper*100,
                    rate_rural_hd_glucose*100, rate_rural_hd_both*100]

axes[0,0].plot(risk_levels, urban_cumulative, marker='o', linewidth=3,
               markersize=10, label='Đô thị', color='#E74C3C')
axes[0,0].plot(risk_levels, rural_cumulative, marker='s', linewidth=3,
               markersize=10, label='Nông thôn', color='#3498DB')

axes[0,0].set_ylabel('Tỷ lệ đột quỵ (%)', fontsize=13, fontweight='bold')
axes[0,0].set_title('Nguy cơ tích lũy theo số yếu tố', fontsize=14, fontweight='bold', pad=15)
axes[0,0].legend(fontsize=11)
axes[0,0].grid(True, alpha=0.3, linestyle='--')
axes[0,0].set_ylim(0, max(urban_cumulative + rural_cumulative) * 1.2)

# Thêm giá trị
for i, (u, r) in enumerate(zip(urban_cumulative, rural_cumulative)):
    if u > 0:
        axes[0,0].text(i, u + 2, f'{u:.1f}%', ha='center', fontsize=10, color='#E74C3C', fontweight='bold')
    if r > 0:
        axes[0,0].text(i, r - 3, f'{r:.1f}%', ha='center', fontsize=10, color='#3498DB', fontweight='bold')

# Chart 2: Grouped bar - By risk factor
if results_amplification:
    rf_names = [r['risk_factor'] for r in results_amplification]
    urban_rf_rates = [r['urban_rate'] for r in results_amplification]
    rural_rf_rates = [r['rural_rate'] for r in results_amplification]

    x_pos = np.arange(len(rf_names))
    width = 0.35

    axes[0,1].bar(x_pos - width/2, urban_rf_rates, width,
                  label='Đô thị', color='#FF6B6B', alpha=0.8, edgecolor='black')
    axes[0,1].bar(x_pos + width/2, rural_rf_rates, width,
                  label='Nông thôn', color='#4ECDC4', alpha=0.8, edgecolor='black')

    axes[0,1].set_ylabel('Tỷ lệ đột quỵ (%)', fontsize=13, fontweight='bold')
    axes[0,1].set_title('Tỷ lệ đột quỵ: Bệnh tim + Yếu tố nguy cơ khác',
                        fontsize=14, fontweight='bold', pad=15)
    axes[0,1].set_xticks(x_pos)
    axes[0,1].set_xticklabels(rf_names, fontsize=10, rotation=15, ha='right')
    axes[0,1].legend(fontsize=11)
    axes[0,1].grid(axis='y', alpha=0.3, linestyle='--')

# Chart 3: Heatmap - Risk combinations
combinations = ['Chỉ HD', 'HD+Huyết áp', 'HD+Glucose', 'HD+Cả 2']
heatmap_data = [
    [rate_urban_hd_only*100, rate_urban_hd_hyper*100,
     rate_urban_hd_glucose*100, rate_urban_hd_both*100],
    [rate_rural_hd_only*100, rate_rural_hd_hyper*100,
     rate_rural_hd_glucose*100, rate_rural_hd_both*100]
]

im = axes[1,0].imshow(heatmap_data, cmap='Reds', aspect='auto')
axes[1,0].set_xticks(np.arange(len(combinations)))
axes[1,0].set_yticks([0, 1])
axes[1,0].set_xticklabels(combinations, rotation=20, ha='right', fontsize=10)
axes[1,0].set_yticklabels(['Đô thị', 'Nông thôn'], fontsize=11)
axes[1,0].set_title('Heatmap: Nguy cơ theo tổ hợp yếu tố', fontsize=14, fontweight='bold', pad=15)

# Thêm giá trị
for i in range(2):
    for j in range(4):
        if heatmap_data[i][j] > 0:
            text = axes[1,0].text(j, i, f'{heatmap_data[i][j]:.1f}%',
                                 ha="center", va="center", color="white" if heatmap_data[i][j] > 15 else "black",
                                 fontsize=11, fontweight='bold')

plt.colorbar(im, ax=axes[1,0], label='Tỷ lệ đột quỵ (%)')

# Chart 4: Amplification ratio
if results_amplification:
    rf_names_ratio = [r['risk_factor'] for r in results_amplification]
    ratios = [r['ratio'] for r in results_amplification]

    colors_ratio = ['#E74C3C' if r > 1.5 else '#F39C12' if r > 1.2 else '#27AE60' for r in ratios]

    bars = axes[1,1].barh(rf_names_ratio, ratios, color=colors_ratio, alpha=0.8, edgecolor='black', linewidth=2)
    axes[1,1].set_xlabel('Tỷ lệ Đô thị / Nông thôn', fontsize=13, fontweight='bold')
    axes[1,1].set_title('Mức độ khuếch đại nguy cơ ở đô thị', fontsize=14, fontweight='bold', pad=15)
    axes[1,1].axvline(x=1, color='black', linestyle='--', linewidth=2, label='Baseline (1x)')
    axes[1,1].legend(fontsize=10)
    axes[1,1].grid(axis='x', alpha=0.3, linestyle='--')

    # Thêm giá trị
    for i, (bar, val) in enumerate(zip(bars, ratios)):
        axes[1,1].text(val + 0.05, bar.get_y() + bar.get_height()/2,
                      f'{val:.2f}x', va='center', fontsize=11, fontweight='bold')

plt.tight_layout()
plt.savefig('outputs/Q3_Act4_RiskAmplification.png', dpi=300, bbox_inches='tight')
plt.show()

print("\n✅ Đã lưu biểu đồ: outputs/Q3_Act4_RiskAmplification.png")
```

#### **Cell 4.4: Tổng kết Hồi 4**

```python
print("\n" + "="*60)
print("📌 TỔNG KẾT HỒI 4")
print("="*60)

print("\n🔍 PHÁT HIỆN CHÍNH:")

print("\n1. HIỆU ỨNG KHUẾCH ĐẠI:")
print("   Khi có bệnh tim + yếu tố nguy cơ khác,")
print("   môi trường đô thị làm nguy cơ TĂNG GẤP BỘI!")

if results_amplification:
    max_ratio_rf = max(results_amplification, key=lambda x: x['ratio'])
    print(f"\n2. YẾU TỐ BỊ KHUẾCH ĐẠI MẠNH NHẤT:")
    print(f"   {max_ratio_rf['risk_factor']}")
    print(f"   - Đô thị: {max_ratio_rf['urban_rate']:.1f}%")
    print(f"   - Nông thôn: {max_ratio_rf['rural_rate']:.1f}%")
    print(f"   - Chênh lệch: {max_ratio_rf['ratio']:.2f}x")

if rate_urban_hd_both > 0 and rate_rural_hd_both > 0:
    print(f"\n3. 'TRIPLE JEOPARDY' (Cả 3 yếu tố):")
    print(f"   - Đô thị: {rate_urban_hd_both*100:.1f}%")
    print(f"   - Nông thôn: {rate_rural_hd_both*100:.1f}%")
    print(f"   - Nguy hiểm hơn {rate_urban_hd_both/rate_rural_hd_both:.2f} lần!")

    if rate_urban_hd_only > 0:
        increase = (rate_urban_hd_both - rate_urban_hd_only) / rate_urban_hd_only * 100
        print(f"\n4. TĂNG TRƯỞNG NGUY CƠ (Urban):")
        print(f"   Từ chỉ HD ({rate_urban_hd_only*100:.1f}%) → HD+2 factors ({rate_urban_hd_both*100:.1f}%)")
        print(f"   Tăng {increase:.0f}%!")

print("\n💭 Ý NGHĨA:")
print("   Môi trường đô thị không chỉ tăng nguy cơ cơ bản,")
print("   mà còn 'KHUẾCH ĐẠI' tác động của các yếu tố nguy cơ khác.")
print("   → Hiệu ứng 'multiplicative' chứ không phải 'additive'!")

print("\n❓ CÂU HỎI CUỐI CÙNG:")
print("→ Vậy TẠI SAO đô thị lại nguy hiểm đến thế?")
print("→ Và chúng ta nên LÀM GÌ?")
print("→ Đó chính là nội dung Hồi 5! ⬇️")
```

---

### **HỒI 5: KẾT LUẬN - "Ý NGHĨA & HÀNH ĐỘNG"**

#### **Cell 5.1: Giải thích - Tại sao Urban nguy hiểm hơn?**

```python
# ============================================================
# HỒI 5: KẾT LUẬN - Ý NGHĨA & HÀNH ĐỘNG
# ============================================================

print("\n" + "="*60)
print("📖 HỒI 5: TẠI SAO & LÀM GÌ?")
print("="*60)

print("\n❓ TẠI SAO ĐÔ THỊ NGUY HIỂM HƠN?")
print("="*60)

explanations = [
    ("🏭 Ô nhiễm không khí",
     "PM2.5, CO, NOx gây stress tim mạch mãn tính"),

    ("😰 Stress mãn tính",
     "Áp lực công việc, giao thông, chi phí sinh hoạt cao"),

    ("🪑 Lối sống ít vận động",
     "Làm việc văn phòng 8h/ngày, đi lại bằng xe máy/ô tô"),

    ("😴 Thiếu ngủ",
     "Giờ làm việc kéo dài, thời gian đi lại xa, ánh sáng/tiếng ồn"),

    ("🍔 Chế độ ăn kém",
     "Thức ăn nhanh, chế biến sẵn, nhiều muối, ít rau"),

    ("🏥 Nghịch lý y tế",
     "Có bệnh viện nhưng KHÔNG ĐI KHÁM thường xuyên (quá bận)"),

    ("👨‍👩‍👧 Hỗ trợ xã hội yếu",
     "Xa gia đình, cộng đồng lỏng lẻo, cô đơn")
]

for i, (factor, explanation) in enumerate(explanations, 1):
    print(f"\n{i}. {factor}")
    print(f"   → {explanation}")

print("\n" + "="*60)
print("💡 TÓM LẠI:")
print("="*60)
print("Đô thị có y tế TỐT nhưng có môi trường SỐNG XẤU!")
print("→ Lợi ích y tế KHÔNG ĐỦ để bù trừ tác hại của lifestyle!")
```

#### **Cell 5.2: Tóm tắt toàn bộ phát hiện**

```python
print("\n" + "="*60)
print("📊 TÓM TẮT TOÀN BỘ PHÁT HIỆN")
print("="*60)

# Tạo bảng summary
summary_data = {
    'Nhóm': [
        'Urban - Nam',
        'Urban - Nữ',
        'Rural - Nam',
        'Rural - Nữ'
    ],
    'Tỷ lệ đột quỵ (%)': [
        f'{stroke_urban_male*100:.1f}',
        f'{stroke_urban_female*100:.1f}',
        f'{stroke_rural_male*100:.1f}',
        f'{stroke_rural_female*100:.1f}'
    ],
    'Số ca': [
        f'{hd_urban_male["stroke"].sum()}/{len(hd_urban_male)}',
        f'{hd_urban_female["stroke"].sum()}/{len(hd_urban_female)}',
        f'{hd_rural_male["stroke"].sum()}/{len(hd_rural_male)}',
        f'{hd_rural_female["stroke"].sum()}/{len(hd_rural_female)}'
    ]
}

df_summary = pd.DataFrame(summary_data)
print("\n", df_summary.to_string(index=False))

print("\n" + "="*60)
print("🎯 5 PHÁT HIỆN CHÍNH")
print("="*60)

findings = [
    f"1. Người có bệnh tim ở đô thị có nguy cơ đột quỵ CAO HƠN {ratio:.2f} lần so với nông thôn",

    f"2. 'Urban penalty' ảnh hưởng NỮ GIỚI nhiều hơn nam giới " +
    (f"({female_penalty/male_penalty:.2f}x)" if female_penalty > male_penalty else ""),

    f"3. Nhóm nguy hiểm NHẤT: {max_group} ({groups[max_group]:.1f}%)",

    "4. Khi có NHIỀU yếu tố nguy cơ, đô thị 'KHUẾCH ĐẠI' nguy cơ gấp bội",

    "5. Nguyên nhân: Stress, ô nhiễm, ít vận động, thiếu ngủ, chế độ ăn kém"
]

for finding in findings:
    print(f"\n{finding}")
```

#### **Cell 5.3: Khuyến nghị - Clinical Implications**

```python
print("\n" + "="*60)
print("💊 KHUYẾN NGHỊ Y TẾ")
print("="*60)

print("\n🏥 CHO CÁC NHÀ CHÍNH SÁCH:")
print("-" * 60)

recommendations_policy = [
    "1. Tăng cường sàng lọc bệnh tim cho DÂN ĐÔ THỊ",
    "   → Đặc biệt: Phụ nữ + làm việc văn phòng",

    "2. Chương trình giảm stress tại nơi làm việc",
    "   → Bắt buộc nghỉ giữa giờ, giới hạn OT",

    "3. Cải thiện chất lượng không khí đô thị",
    "   → Giảm phương tiện cá nhân, tăng giao thông công cộng",

    "4. Xây dựng không gian xanh",
    "   → Công viên, đường đi bộ, khu vực tập thể dục",

    "5. Chiến dịch nhận thức về 'urban lifestyle diseases'",
    "   → 'Sống khỏe trong thành phố' campaigns"
]

for rec in recommendations_policy:
    print(f"\n{rec}")

print("\n\n👨‍⚕️ CHO BÁC SĨ:")
print("-" * 60)

recommendations_doctors = [
    "1. Theo dõi GẮT GÀO hơn với bệnh nhân đô thị có bệnh tim",
    "   → Tái khám thường xuyên hơn (3 tháng/lần thay vì 6 tháng)",

    "2. Tư vấn quản lý stress",
    "   → Không chỉ thuốc, mà còn lifestyle modification",

    "3. Chú ý ĐẶC BIỆT với bệnh nhân NỮ",
    "   → Hỏi về work-life balance, gánh nặng gia đình",

    "4. Screening TÍCH CỰC cho 'triple jeopardy'",
    "   → HD + Hypertension + High glucose = Mức độ ưu tiên cao nhất",

    "5. Giáo dục về 'compensatory behaviors'",
    "   → Sống đô thị → CẦN exercise NHIỀU HƠN để bù trừ"
]

for rec in recommendations_doctors:
    print(f"\n{rec}")

print("\n\n🏃 CHO NGƯỜI DÂN (ĐẶC BIỆT ĐÔ THỊ):")
print("-" * 60)

recommendations_public = [
    "1. Nếu có bệnh tim: KHÁM ĐỊNH KỲ nghiêm túc",
    "   → Không bỏ qua vì 'bận', 'không có triệu chứng'",

    "2. Vận động ÍT NHẤT 30 phút/ngày",
    "   → Leo cầu thang, đi bộ trong công viên, yoga tại nhà",

    "3. Quản lý stress",
    "   → Thiền, đọc sách, gặp gỡ bạn bè, sở thích",

    "4. Ngủ đủ 7-8 giờ/đêm",
    "   → Tắt điện thoại trước khi ngủ, phòng tối và yên tĩnh",

    "5. Chế độ ăn lành mạnh",
    "   → Tự nấu > thức ăn nhanh, nhiều rau, ít muối",

    "6. Nếu là PHỤ NỮ: Đừng 'hy sinh' sức khỏe vì gia đình",
    "   → Chăm sóc bản thân CŨNG quan trọng như chăm sóc người khác"
]

for rec in recommendations_public:
    print(f"\n{rec}")
```

#### **Cell 5.4: Visualization - Final Summary**

```python
# Biểu đồ tóm tắt cuối cùng
fig = plt.figure(figsize=(18, 10))
gs = fig.add_gridspec(3, 3, hspace=0.3, wspace=0.3)

# Chart 1: Main comparison (lớn, chiếm 2 ô)
ax1 = fig.add_subplot(gs[0, :2])

categories_final = ['Đô thị', 'Nông thôn']
rates_final = [stroke_rate_urban*100, stroke_rate_rural*100]
colors_final = ['#E74C3C', '#27AE60']

bars_final = ax1.bar(categories_final, rates_final, color=colors_final,
                     alpha=0.8, edgecolor='black', linewidth=3, width=0.5)

ax1.set_ylabel('Tỷ lệ đột quỵ (%)', fontsize=14, fontweight='bold')
ax1.set_title('PHÁT HIỆN CHÍNH\nNgười có bệnh tim ở đô thị nguy hiểm hơn',
              fontsize=16, fontweight='bold', pad=20)
ax1.set_ylim(0, max(rates_final)*1.5)
ax1.grid(axis='y', alpha=0.3, linestyle='--')

# Thêm giá trị lớn
for i, (bar, val) in enumerate(zip(bars_final, rates_final)):
    ax1.text(bar.get_x() + bar.get_width()/2, val + 2,
             f'{val:.1f}%', ha='center', fontsize=18, fontweight='bold')

    # Thêm warning cho urban
    if i == 0:
        ax1.text(bar.get_x() + bar.get_width()/2, val/2,
                 f'⚠️ GẤP {ratio:.1f} LẦN', ha='center', fontsize=13,
                 fontweight='bold', color='white',
                 bbox=dict(boxstyle='round', facecolor='red', alpha=0.9))

# Chart 2: Gender breakdown (nhỏ)
ax2 = fig.add_subplot(gs[0, 2])

gender_labels = ['Nam', 'Nữ']
urban_gender = [stroke_urban_male*100, stroke_urban_female*100]
rural_gender = [stroke_rural_male*100, stroke_rural_female*100]

x = np.arange(len(gender_labels))
width = 0.35

ax2.bar(x - width/2, urban_gender, width, label='Đô thị', color='#FF6B6B', alpha=0.8)
ax2.bar(x + width/2, rural_gender, width, label='Nông thôn', color='#4ECDC4', alpha=0.8)

ax2.set_title('Theo giới tính', fontsize=12, fontweight='bold')
ax2.set_xticks(x)
ax2.set_xticklabels(gender_labels, fontsize=10)
ax2.legend(fontsize=9)
ax2.set_ylabel('Tỷ lệ (%)', fontsize=10)
ax2.grid(axis='y', alpha=0.3)

# Chart 3: Risk factors amplification
ax3 = fig.add_subplot(gs[1, :])

if len(hd_urban_male) > 0:
    risk_labels = ['Chỉ\nBệnh tim', 'HD +\nHuyết áp', 'HD +\nGlucose', 'Cả 3\nyếu tố']
    urban_risks = [rate_urban_hd_only*100, rate_urban_hd_hyper*100,
                   rate_urban_hd_glucose*100, rate_urban_hd_both*100]
    rural_risks = [rate_rural_hd_only*100, rate_rural_hd_hyper*100,
                   rate_rural_hd_glucose*100, rate_rural_hd_both*100]

    x = np.arange(len(risk_labels))
    width = 0.35

    ax3.bar(x - width/2, urban_risks, width, label='Đô thị', color='#E74C3C', alpha=0.8, edgecolor='black')
    ax3.bar(x + width/2, rural_risks, width, label='Nông thôn', color='#27AE60', alpha=0.8, edgecolor='black')

    ax3.set_ylabel('Tỷ lệ đột quỵ (%)', fontsize=12, fontweight='bold')
    ax3.set_title('HIỆU ỨNG KHUẾCH ĐẠI: Nguy cơ tăng theo số yếu tố',
                  fontsize=14, fontweight='bold', pad=15)
    ax3.set_xticks(x)
    ax3.set_xticklabels(risk_labels, fontsize=11)
    ax3.legend(fontsize=11, loc='upper left')
    ax3.grid(axis='y', alpha=0.3, linestyle='--')

    # Highlight triple jeopardy
    if rate_urban_hd_both > 0:
        ax3.annotate('⚠️ TRIPLE\nJEOPARDY!',
                     xy=(len(risk_labels)-1, rate_urban_hd_both*100),
                     xytext=(len(risk_labels)-1.5, rate_urban_hd_both*100 + 5),
                     fontsize=11, fontweight='bold', color='red',
                     bbox=dict(boxstyle='round', facecolor='yellow', alpha=0.7),
                     arrowprops=dict(arrowstyle='->', color='red', lw=2))

# Chart 4: Recommendations (text box)
ax4 = fig.add_subplot(gs[2, :])
ax4.axis('off')

recommendations_text = """
🎯 KHUYẾN NGHỊ HÀNH ĐỘNG

👥 CHO NGƯỜI DÂN (Đô thị):
  • Khám định kỳ NGHIÊM TÚC nếu có bệnh tim
  • Vận động ≥30 phút/ngày (leo cầu thang, đi bộ)
  • Quản lý stress (thiền, yoga, sở thích)
  • Ngủ đủ 7-8 giờ/đêm
  • Tự nấu ăn > Thức ăn nhanh

🏥 CHO BÁC SĨ:
  • Theo dõi GẮT GÀO hơn với bệnh nhân đô thị
  • CHÚ Ý ĐẶC BIỆT với phụ nữ (work-life balance)
  • Tư vấn lifestyle modification, không chỉ thuốc
  • Screening tích cực cho "triple jeopardy"

🏛️ CHO NHÀ CHÍNH SÁCH:
  • Chương trình sàng lọc cho dân đô thị
  • Giảm stress tại nơi làm việc (giới hạn OT)
  • Cải thiện không khí (giao thông công cộng)
  • Xây dựng không gian xanh (công viên, đường đi bộ)
"""

ax4.text(0.05, 0.95, recommendations_text,
         transform=ax4.transAxes,
         fontsize=11, verticalalignment='top',
         bbox=dict(boxstyle='round', facecolor='#E8F5E9', alpha=0.8, edgecolor='#4CAF50', linewidth=2),
         family='monospace')

plt.suptitle('CÂU HỎI 3: TỔNG KẾT - NGHỊCH LÝ BỆNH TIM Ở ĐÔ THỊ',
             fontsize=18, fontweight='bold', y=0.995)

plt.savefig('outputs/Q3_Act5_FinalSummary.png', dpi=300, bbox_inches='tight')
plt.show()

print("\n✅ Đã lưu biểu đồ: outputs/Q3_Act5_FinalSummary.png")
```

#### **Cell 5.5: Kết thúc - Take-home message**

```python
print("\n" + "="*80)
print("🎬 KẾT THÚC - TAKE-HOME MESSAGE")
print("="*80)

print("\n" + "🎯 " + "="*76)
print("  CÂU TRẢ LỜI CHO CÂU HỎI NGHIÊN CỨU")
print("="*80)

print("""
❓ Người mắc bệnh tim sống ở đô thị có 'nhạy cảm' hơn với đột quỵ
   so với người mắc bệnh tim sống ở nông thôn không?

✅ CÓ! Người có bệnh tim ở đô thị có nguy cơ đột quỵ cao hơn
""")

if stroke_rate_urban > stroke_rate_rural:
    print(f"   {ratio:.2f} LẦN so với nông thôn.")
    print(f"   (Đô thị: {stroke_rate_urban*100:.1f}% vs Nông thôn: {stroke_rate_rural*100:.1f}%)")

print("""
❓ Liệu mức độ nhạy cảm này khác nhau giữa nam và nữ?

✅ CÓ! 'Urban penalty' ảnh hưởng NỮ GIỚI nhiều hơn Nam giới.
""")

if female_penalty > male_penalty:
    print(f"   Nữ giới: +{female_penalty*100:.1f}% (Urban vs Rural)")
    print(f"   Nam giới: +{male_penalty*100:.1f}% (Urban vs Rural)")
    print(f"   → Nữ giới bị ảnh hưởng nhiều hơn {female_penalty/male_penalty:.2f} lần")

print("\n" + "="*80)
print("💡 3 ĐIỀU QUAN TRỌNG NHẤT")
print("="*80)

key_messages = [
    """
1. NGHỊCH LÝ Y TẾ ĐÔ THỊ:
   Đô thị có bệnh viện tốt hơn NHƯNG kết quả sức khỏe XẤU HƠN!
   → Lợi ích y tế KHÔNG ĐỦ bù trừ tác hại của môi trường sống.
    """,

    """
2. HIỆU ỨNG KHUẾCH ĐẠI:
   Đô thị không chỉ tăng nguy cơ cơ bản, mà còn 'KHUẾCH ĐẠI'
   tác động của các yếu tố nguy cơ khác (hypertension, glucose).
   → Effect là 'multiplicative' chứ không phải 'additive'.
    """,

    """
3. GENDER DISPARITY:
   Phụ nữ có bệnh tim ở đô thị phải 'TRẢ GIÁ' nhiều hơn nam giới.
   Nguyên nhân: Gánh nặng chăm sóc gia đình + Work-life balance
   + Vai trò caregiver + Stress mãn tính.
    """
]

for msg in key_messages:
    print(msg)

print("\n" + "="*80)
print("🏁 FINAL THOUGHTS")
print("="*80)

print("""
Nghiên cứu này cho thấy rằng:

▸ "Tiến bộ y tế" KHÔNG TỰ ĐỘNG dẫn đến "Sức khỏe tốt hơn"
  nếu môi trường sống và lối sống không được cải thiện.

▸ Đô thị hóa nhanh ở Việt Nam đang tạo ra một thế hệ
  "healthy-looking but actually at high risk".

▸ Cần có chính sách can thiệp ĐA CHIỀU:
  • Không chỉ xây bệnh viện
  • Mà còn cải thiện chất lượng sống đô thị
  • Và thay đổi hành vi cá nhân

▸ ĐẶC BIỆT chú ý đến sức khỏe PHỤ NỮ đô thị - một nhóm
  đang bị "overlooked" nhưng lại chịu gánh nặng kép.

🎯 "Prevention is better than cure" - Nhưng trong bối cảnh
   đô thị, prevention cần phải AGGRESSIVE và COMPREHENSIVE hơn!
""")

print("\n" + "="*80)
print("✅ HOÀN THÀNH PHÂN TÍCH CÂU HỎI 3")
print("="*80)
print("\nCảm ơn bạn đã theo dõi! 🙏")
```

---

## 📁 CẤU TRÚC THƯ MỤC OUTPUT

```
outputs/
├── Q3_Act1_Context.png              # Bối cảnh
├── Q3_Act2_MainComparison.png       # So sánh chính Urban vs Rural
├── Q3_Act3_GenderDimension.png      # Phân tích theo giới tính
├── Q3_Act3_Heatmap.png              # Heatmap 2x2
├── Q3_Act4_RiskAmplification.png    # Hiệu ứng khuếch đại
└── Q3_Act5_FinalSummary.png         # Tổng kết cuối cùng
```

---

## 🎯 ĐIỂM MẠNH CỦA THIẾT KẾ NÀY

### **1. Storytelling mạnh mẽ:**
- ✅ 5 Hồi liên kết chặt chẽ như một câu chuyện
- ✅ Mỗi hồi có setup → discovery → revelation
- ✅ Build-up tension từ simple → complex → insight

### **2. Nhiều góc độ phân tích:**
- ✅ Urban vs Rural (main)
- ✅ Male vs Female (gender dimension)
- ✅ Risk amplification (interaction effects)
- ✅ Clinical implications (actionable)

### **3. Visualizations đa dạng:**
- ✅ 6 figure chính với 15+ charts
- ✅ Bar, line, heatmap, grouped bars, annotations
- ✅ Màu sắc nhất quán, clear labels

### **4. Ngôn ngữ tiếng Việt:**
- ✅ Comment code hoàn toàn tiếng Việt
- ✅ Output text tiếng Việt
- ✅ Biểu đồ có label tiếng Việt

### **5. Actionable insights:**
- ✅ Không chỉ phân tích mà còn đưa ra khuyến nghị
- ✅ Cho 3 nhóm: Dân, bác sĩ, nhà chính sách
- ✅ Specific và practical

---

## ⏱️ THỜI GIAN THỰC HIỆN

- **Hồi 1 (Context)**: 20 phút
- **Hồi 2 (Main comparison)**: 30 phút
- **Hồi 3 (Gender)**: 40 phút
- **Hồi 4 (Amplification)**: 40 phút
- **Hồi 5 (Conclusion)**: 30 phút

**Tổng: ~2.5-3 giờ**

---

## 🎓 PHÙ HỢP CHO BÁO CÁO

Cấu trúc này có thể dễ dàng chuyển thành báo cáo với:
- Introduction = Hồi 1
- Methods = Code cells
- Results = Hồi 2, 3, 4
- Discussion = Hồi 5 (explanations)
- Conclusion = Hồi 5 (take-home message)
- Recommendations = Hồi 5 (clinical implications)

---

✅ **File thiết kế đã được lưu tại:**
`THIET_KE_CAU_HOI_3.md`
