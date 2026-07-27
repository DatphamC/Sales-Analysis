# 🛍️ Sales Data Analysis — 2019

Phân tích **185.950 giao dịch bán lẻ sản phẩm điện tử** trong năm 2019, gộp từ 12 file CSV theo tháng.
Project đi qua toàn bộ quy trình: gộp dữ liệu → làm sạch → phân tích → trực quan hoá → rút ra khuyến nghị kinh doanh.

**Tổng doanh thu: $34.492.035,97**

---

## 📁 Cấu trúc project

```
Sales-Analysis/
├── report.ipynb              # Notebook phân tích chính
├── README.md
├── requirements.txt
└── Data/
    ├── sales2019_1.csv       # 12 file dữ liệu gốc theo tháng
    ├── ...
    ├── sales2019_12.csv
    └── sales2019_all.csv     # File gộp — sinh ra khi chạy Task 1, không commit lên repo
```

Dữ liệu gốc gồm 6 cột: `Order ID`, `Product`, `Quantity Ordered`, `Price Each`, `Order Date`, `Purchase Address`.

---

## ⚙️ Tools & Libraries

- **Python 3.11**
- **pandas** — xử lý và làm sạch dữ liệu
- **matplotlib** — trực quan hoá
- **glob / re** — quét và sắp xếp file theo tháng
- **itertools / collections** — phân tích cặp sản phẩm mua kèm
- **Jupyter Notebook** — môi trường phân tích và trình bày

---

## 🧩 Quy trình

### Task 1 — Import và gộp dữ liệu
- Quét 12 file `Data/sales2019_1.csv` … `Data/sales2019_12.csv`
- Sắp xếp theo số tháng bằng regex thay vì thứ tự alphabet (tránh `10` đứng trước `2`)
- Gộp thành `Data/sales2019_all.csv` — 186.850 dòng

### Task 2 — Làm sạch và tiền xử lý
- Loại **545 dòng trống** và **355 dòng tiêu đề lặp** lẫn vào giữa dữ liệu khi nối file → còn **185.950 dòng**
- Ép kiểu: `Quantity Ordered` → int, `Price Each` → float64, `Order Date` → datetime
- Tạo cột phái sinh: `Month`, `Hour`, `Sales` = `Quantity × Price`, và `City` tách từ `Purchase Address`

### Task 3 — Phân tích và trả lời câu hỏi nghiệp vụ
5 câu hỏi, mỗi câu kèm bảng số liệu và biểu đồ.

---

## 📈 Kết quả chính

| # | Câu hỏi | Trả lời |
|---|---|---|
| 1 | Tháng bán tốt nhất | **Tháng 12** — $4.613.443 |
| 2 | Thành phố dẫn đầu | **San Francisco (CA)** — $8.262.204 |
| 3 | Giờ chạy quảng cáo | **10–11h** và **18–19h** |
| 4 | Combo phổ biến nhất | **iPhone + Lightning Charging Cable** — 1.011 lần |
| 5 | Sản phẩm bán chạy nhất | **AAA Batteries (4-pack)** — 31.017 chiếc |

### Chi tiết

**Doanh thu theo tháng.** Tháng 12 dẫn đầu nhờ mùa lễ, gấp hơn 2,5 lần tháng 1 — tháng thấp nhất
($1.822.257). Hai đỉnh phụ vào tháng 4 và tháng 10.

**Doanh thu theo thành phố.** San Francisco chiếm ~24% tổng doanh thu, cao hơn Los Angeles (hạng 2)
khoảng 50%. Ba thành phố dẫn đầu đều là trung tâm công nghệ / tài chính lớn.

**Khung giờ mua hàng.** Phân bố có hình **hai bướu** rõ rệt: đỉnh trưa 11–13h và đỉnh tối 18–20h,
trong đó **19h là giờ cao điểm nhất** (12.905 đơn). Đáy rơi vào 02–05h (dưới 1.400 đơn/giờ).
Nên đặt quảng cáo ngay *trước* hai đỉnh này.

**Sản phẩm mua kèm.** Toàn bộ top 10 đều theo mô-típ *điện thoại + phụ kiện tương thích*, và cáp sạc
luôn khớp đúng chuẩn của máy (Lightning cho iPhone, USB-C cho Google/Vareebadd) — hành vi mua kèm
bắt buộc, rất phù hợp để dựng gói bundle.

**Sản phẩm bán chạy.** Tương quan hạng giữa giá và số lượng bán là **−0,78**: giá càng rẻ bán càng
nhiều. Nhưng bán chạy ≠ đóng góp doanh thu lớn — Macbook Pro Laptop chỉ bán 4.728 chiếc mà mang lại
doanh thu cao nhất ($8,04 triệu), còn AAA Batteries bán gấp 6,5 lần nhưng doanh thu thấp nhất ($92.741).

---

## 📊 Biểu đồ trong notebook

- Doanh thu theo tháng (bar chart)
- Doanh thu theo thành phố (bar chart)
- Số đơn hàng và doanh thu theo giờ (2 line charts)
- Top 10 cặp sản phẩm mua kèm (horizontal bar chart)
- Số lượng bán vs. giá trung bình theo sản phẩm (dual-axis)

---

## 🚀 Cách chạy

```bash
git clone https://github.com/DatphamC/Sales-Analysis.git
cd Sales-Analysis
```

```bash
pip install -r requirements.txt
```

```bash
jupyter notebook report.ipynb
```

Notebook dùng **đường dẫn tương đối**, nên cần mở Jupyter ngay tại thư mục project.
Chạy `Run All` là tái tạo được toàn bộ kết quả, kể cả file `Data/sales2019_all.csv`.

---

## 🔍 Một vài chi tiết kỹ thuật

Ba điểm dễ sai mà notebook xử lý riêng:

**Glob pattern.** Dùng `sales2019_[0-9]*.csv` thay vì `sales2019_*.csv`. Pattern thứ hai sẽ khớp luôn
file kết quả `sales2019_all.csv`, khiến dữ liệu bị nhân đôi mỗi lần chạy lại.

**Kiểu float.** Giữ `Price Each` ở `float64`. Nếu downcast xuống `float32` thì chỉ còn ~7 chữ số có
nghĩa trong khi doanh thu cộng dồn lên tới 8 chữ số — giá 149.99 bị lưu thành 149.990005 và tổng bị lệch.

**Trùng tên thành phố.** Dataset có **hai thành phố tên Portland** (OR và ME). Nếu chỉ tách tên thành
phố thì doanh thu hai nơi bị cộng gộp; notebook ghép thêm mã bang thành `Portland (OR)` — $1.870.732
và `Portland (ME)` — $449.758, hai thị trường có quy mô hoàn toàn khác nhau.

---

## 🧠 Hướng phát triển tiếp

- Phân tích theo doanh thu thay vì số lượng để xác định sản phẩm chủ lực thực sự
- Tính giá trị đơn hàng trung bình (AOV) theo thành phố
- Market basket analysis đầy đủ (support / confidence / lift) thay vì chỉ đếm tần suất cặp
- Xem xét yếu tố mùa vụ riêng cho từng nhóm sản phẩm

---

## 👤 Tác giả

**Dat Pham** — Data Analyst | Python, SQL, Excel
[GitHub](https://github.com/DatphamC)
