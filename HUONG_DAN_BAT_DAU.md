# HƯỚNG DẪN BẮT ĐẦU DỰ ÁN
# GETTING STARTED GUIDE

---

## 🎯 BƯỚC 1: CÀI ĐẶT MÔI TRƯỜNG

### 1.1 Kiểm tra Python

Mở terminal/command prompt và chạy:

```bash
python --version
```

Yêu cầu: Python 3.8 trở lên

Nếu chưa có, tải tại: https://www.python.org/downloads/

### 1.2 Cài đặt thư viện

```bash
# Di chuyển vào thư mục dự án
cd "d:\LẬP TRÌNH\Năm 4\LTKHDL\ĐỒ ÁN CUỐI KÌ"

# Cài đặt tất cả thư viện cần thiết
pip install -r requirements.txt
```

**Lưu ý**: Quá trình cài đặt có thể mất 5-10 phút.

### 1.3 Kiểm tra cài đặt

```bash
# Kiểm tra Jupyter đã cài đặt chưa
jupyter --version

# Nếu chưa có:
pip install jupyter
```

---

## 📥 BƯỚC 2: TẢI DATASET

### 2.1 Truy cập Kaggle

1. Mở trình duyệt, truy cập: https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset
2. Đăng nhập tài khoản Kaggle (hoặc tạo tài khoản mới - miễn phí)

### 2.2 Tải dữ liệu

1. Nhấn nút **"Download"** (góc trên bên phải)
2. File tải về: `healthcare-dataset-stroke-data.csv` (khoảng 40KB)
3. Chờ tải xong

### 2.3 Đặt file vào đúng vị trí

**Quan trọng**: Đặt file CSV vào thư mục `data/`

```
ĐỒ ÁN CUỐI KÌ/
├── data/
│   └── healthcare-dataset-stroke-data.csv  ← ĐẶT FILE VÀO ĐÂY
├── notebooks/
│   └── stroke_analysis.ipynb
├── README.md
└── requirements.txt
```

**Cách đặt file**:
- Di chuyển file `healthcare-dataset-stroke-data.csv` từ thư mục Downloads
- Paste vào thư mục `d:\LẬP TRÌNH\Năm 4\LTKHDL\ĐỒ ÁN CUỐI KÌ\data\`

---

## 🚀 BƯỚC 3: KHỞI ĐỘNG JUPYTER NOTEBOOK

### 3.1 Mở terminal tại thư mục dự án

```bash
# Windows: Mở Command Prompt hoặc PowerShell tại thư mục dự án
cd "d:\LẬP TRÌNH\Năm 4\LTKHDL\ĐỒ ÁN CUỐI KÌ"
```

### 3.2 Khởi động Jupyter

```bash
jupyter notebook
```

Hoặc:

```bash
jupyter lab
```

### 3.3 Trình duyệt sẽ tự động mở

- URL: http://localhost:8888/
- Giao diện Jupyter sẽ hiển thị

### 3.4 Mở notebook

1. Trong giao diện Jupyter, click vào thư mục `notebooks/`
2. Click vào file `stroke_analysis.ipynb`
3. Notebook sẽ mở

---

## ✅ BƯỚC 4: CHẠY THỬ NOTEBOOK

### 4.1 Chạy cell đầu tiên

1. Click vào cell đầu tiên (import libraries)
2. Nhấn **Shift + Enter** để chạy
3. Đợi khoảng 5-10 giây
4. Nếu thấy "✅ Đã import tất cả thư viện thành công!" → OK!

### 4.2 Chạy cell load data

1. Click vào cell "Load Dataset"
2. Nhấn **Shift + Enter**
3. Nếu thấy "✅ Đã tải dữ liệu thành công!" → Hoàn hảo!

### 4.3 Nếu gặp lỗi

**Lỗi: "FileNotFoundError"**
```
❌ Nguyên nhân: File CSV chưa đúng vị trí
✅ Giải pháp: Kiểm tra lại BƯỚC 2.3
```

**Lỗi: "ModuleNotFoundError"**
```
❌ Nguyên nhân: Thiếu thư viện
✅ Giải pháp: Chạy lại `pip install -r requirements.txt`
```

---

## 📋 BƯỚC 5: CẬP NHẬT THÔNG TIN NHÓM

### 5.1 Điền thông tin vào README.md

Mở file `README.md`, tìm phần "Thông Tin Nhóm" và điền:

```markdown
### Thành viên
- **Thành viên 1**: [Họ tên đầy đủ] - [MSSV] - [Email]
  - Phân công: Data Collection, Data Exploration
  - Đóng góp: 33%

- **Thành viên 2**: [Họ tên đầy đủ] - [MSSV] - [Email]
  - Phân công: Question Formulation, Analysis Q1-Q3
  - Đóng góp: 33%

- **Thành viên 3**: [Họ tên đầy đủ] - [MSSV] - [Email]
  - Phân công: ML Model, Summary, Reflections
  - Đóng góp: 34%
```

### 5.2 Điền thông tin vào Notebook

Mở notebook, tìm cell "THÔNG TIN NHÓM" và điền tương tự.

---

## 📊 BƯỚC 6: BẮT ĐẦU PHÂN TÍCH

### 6.1 Xác định số lượng thành viên nhóm

**Quan trọng**: Nhóm bạn có bao nhiêu người?

- Nếu **n = 2 người** → Cần **2×2 = 4 câu hỏi** (ít nhất 1 câu ML)
- Nếu **n = 3 người** → Cần **2×3 = 6 câu hỏi** (ít nhất 1 câu ML)
- Nếu **n = 4 người** → Cần **2×4 = 8 câu hỏi** (ít nhất 1 câu ML)

### 6.2 Roadmap theo thứ tự

✅ **Tuần 1** (Đã xong - Setup):
- [x] Tạo cấu trúc dự án
- [x] Tải dataset
- [x] Setup môi trường

📌 **Tuần 2** (Data Exploration):
- [ ] Chạy phần 2.1: Tổng quan dataset
- [ ] Chạy phần 2.2: Phân tích cột số
- [ ] Chạy phần 2.3: Phân tích cột categorical
- [ ] Chạy phần 2.4: Phân tích missing data
- [ ] Chạy phần 2.5: Correlations
- [ ] Viết phần 2.6: Quan sát ban đầu

📌 **Tuần 3** (Questions & Analysis):
- [ ] Xây dựng 2×n câu hỏi nghiên cứu
- [ ] Phân tích Q1, Q2, Q3
- [ ] Phân tích Q4, Q5 (ML), Q6

📌 **Tuần 4** (Finalize):
- [ ] Summary & Conclusions
- [ ] Individual Reflections
- [ ] Review toàn bộ notebook
- [ ] Hoàn thiện README
- [ ] Kiểm tra lần cuối

---

## 🎓 CÁC TIPS QUAN TRỌNG

### ✅ DOs (Nên làm):

1. **Comment code bằng tiếng Việt**:
   ```python
   # Tính trung bình tuổi của nhóm bị đột quỵ
   # Calculate average age of stroke patients
   stroke_avg_age = df[df['stroke'] == 1]['age'].mean()
   ```

2. **Markdown cell giải thích trước code cell**:
   ```markdown
   ## Phân tích tuổi và đột quỵ

   Chúng ta sẽ so sánh tuổi trung bình giữa nhóm bị đột quỵ và không bị đột quỵ
   để xem tuổi có phải là yếu tố nguy cơ quan trọng không.
   ```

3. **Visualizations có labels đầy đủ**:
   ```python
   plt.title('Phân Bố Tuổi Theo Tình Trạng Đột Quỵ\nAge Distribution by Stroke Status')
   plt.xlabel('Tuổi (Age)')
   plt.ylabel('Số lượng (Count)')
   ```

4. **Cite số liệu cụ thể khi diễn giải**:
   ```markdown
   Kết quả cho thấy tuổi trung bình của nhóm bị đột quỵ là **67.6 tuổi**,
   cao hơn đáng kể so với nhóm không bị đột quỵ (42.1 tuổi), với p-value < 0.001.
   ```

### ❌ DON'Ts (Không nên làm):

1. ❌ Code không có explanation
2. ❌ Plots không có title/labels
3. ❌ Kết luận chung chung không có số liệu
4. ❌ Copy-paste code không hiểu
5. ❌ Notebook không chạy được từ đầu đến cuối

---

## 🆘 KHI CẦN TRỢ GIÚP

### Tài nguyên học tập:

1. **Pandas**: https://pandas.pydata.org/docs/
2. **Matplotlib**: https://matplotlib.org/stable/tutorials/index.html
3. **Seaborn**: https://seaborn.pydata.org/tutorial.html
4. **Scikit-learn**: https://scikit-learn.org/stable/tutorial/index.html

### Cộng đồng:

1. **Stack Overflow**: Tìm kiếm lỗi bằng tiếng Anh
2. **Kaggle Kernels**: Xem cách người khác phân tích dataset này
3. **Google**: "[tên lỗi] + python"

### Liên hệ:

- Email nhóm: [điền email]
- Group chat: [điền link nếu có]

---

## 📝 CHECKLIST TRƯỚC KHI NỘP

- [ ] Notebook chạy được từ đầu đến cuối (Run All Cells)
- [ ] Tất cả visualizations có title, xlabel, ylabel, legend
- [ ] Mỗi analysis section có markdown explanation
- [ ] Có đủ 2×n câu hỏi nghiên cứu
- [ ] Có ít nhất 1 câu hỏi ML với ≥2 models
- [ ] Mỗi câu hỏi có ≥2 visualizations
- [ ] Kết quả có số liệu cụ thể, không chung chung
- [ ] Có phần Limitations
- [ ] Có Individual Reflections
- [ ] README.md hoàn chỉnh
- [ ] File structure đúng format

---

## 🎉 SẴN SÀNG BẮT ĐẦU!

Bây giờ bạn đã sẵn sàng! Hãy:

1. ✅ Kiểm tra lại tất cả các bước trên
2. ✅ Mở Jupyter Notebook
3. ✅ Bắt đầu với phần Data Exploration
4. ✅ Làm từng bước một, không vội vàng
5. ✅ Hỏi khi gặp khó khăn

**Chúc bạn làm đồ án thành công! 🚀**

---

*Last updated: [Ngày tháng năm]*
