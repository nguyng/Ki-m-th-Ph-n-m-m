# ĐỀ THI GIỮA KỲ – MÔN KIỂM THỬ PHẦN MỀM
## **ĐỀ 01 – KỊCH BẢN 2**
### Thời gian: 60 phút | Được sử dụng tài liệu: Không

---

## CÂU 1 (6 ĐIỂM) – KIỂM THỬ HỘP ĐEN (Black-box Testing)

### Đặc tả bài toán: Hệ thống xét học bổng sinh viên

Một trường đại học xét học bổng cho sinh viên dựa trên **ba điều kiện** sau:

- **C1 – Điểm trung bình tích lũy (GPA):** Đạt từ **3.2 trở lên** (thang 4.0) là điều kiện học lực tốt.
- **C2 – Số tín chỉ đã hoàn thành:** Đã tích lũy từ **60 tín chỉ trở lên**.
- **C3 – Tình trạng kỷ luật:** Không có cảnh cáo kỷ luật trong học kỳ hiện tại.

**Các mức học bổng:**

| Điều kiện thỏa mãn | Mức học bổng |
|:--|:--|
| Cả 3 điều kiện đều đạt | Học bổng Xuất sắc – 100% học phí |
| Chỉ C1 và C3 đạt (thiếu C2) | Học bổng Khuyến khích – 50% học phí |
| Chỉ C1 đạt (thiếu C2 hoặc C3) | Học bổng Tiềm năng – 20% học phí |
| Không đạt C1 | Không được học bổng |

---

### Áp dụng kỹ thuật Kiểm thử Bảng quyết định (Decision Table Testing) (6 điểm)

**Yêu cầu:**
1. Xác định các điều kiện (Conditions) và hành động (Actions) của bài toán.
2. Xây dựng **Bảng quyết định (Decision Table)** đầy đủ với tất cả các tổ hợp điều kiện có thể.
3. Thiết kế **ca kiểm thử (Test Cases)** tương ứng cho mỗi quy tắc (rule) trong bảng quyết định. Ghi rõ: Mã TC, dữ liệu đầu vào, kết quả mong đợi.

---

## CÂU 2 (4 ĐIỂM) – KIỂM THỬ HỘP TRẮNG (White-box Testing)

### Mã nguồn:

```c
int classify(int score, int attendance, int passed)
{
    int result = 0;
    if (score >= 5 || (attendance >= 80 && passed == 1))
    {
        if (score >= 8)
            result = 3;
        else if (score >= 6)
            result = 2;
        else
            result = 1;
    }
    return result;
}
```

> **Chú thích:** `score`: Điểm số (0–10), `attendance`: % chuyên cần (0–100), `passed`: Đã nộp đủ bài tập (1: có, 0: không).
> Trả về: 3 = Giỏi, 2 = Khá, 1 = Trung bình, 0 = Không đạt.

**Yêu cầu:**
1. Vẽ Đồ thị luồng điều khiển (CFG) của hàm trên. Đánh số nút rõ ràng.
2. Tính độ phức tạp Cyclomatic V(G) bằng hai công thức khác nhau.
3. Liệt kê tất cả các đường thi hành (paths) thỏa mãn tiêu chí **Bao phủ nhánh và điều kiện (Branch & Condition Coverage)**.
4. Thiết kế bảng ca kiểm thử tương ứng (ghi rõ Input, nhánh/điều kiện được bao phủ, kết quả mong đợi).

---

### Hết

---
---

# LỜI GIẢI CHI TIẾT – ĐỀ 01 KỊCH BẢN 2

---

## CÂU 1 – LỜI GIẢI (6 điểm)

### Bước 1: Xác định Điều kiện và Hành động

**Các điều kiện (Conditions):**

| Ký hiệu | Điều kiện |
|:--:|:--|
| **C1** | GPA ≥ 3.2 (T/F) |
| **C2** | Tín chỉ ≥ 60 (T/F) |
| **C3** | Không có cảnh cáo kỷ luật (T/F) |

**Các hành động (Actions):**

| Ký hiệu | Hành động |
|:--:|:--|
| **A1** | Học bổng Xuất sắc – 100% học phí |
| **A2** | Học bổng Khuyến khích – 50% học phí |
| **A3** | Học bổng Tiềm năng – 20% học phí |
| **A4** | Không được học bổng |

---

### Bước 2: Bảng quyết định (Decision Table)

3 điều kiện nhị phân → tối đa 2³ = 8 tổ hợp. Phân tích theo đặc tả:

| Điều kiện / Hành động | R1 | R2 | R3 | R4 | R5 | R6 | R7 | R8 |
|:--|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| **C1: GPA ≥ 3.2** | T | T | T | T | F | F | F | F |
| **C2: TC ≥ 60** | T | T | F | F | T | T | F | F |
| **C3: Không KL** | T | F | T | F | T | F | T | F |
| **A1: XS – 100%** | **X** | | | | | | | |
| **A2: KK – 50%** | | | **X** | | | | | |
| **A3: TN – 20%** | | **X** | | **X** | | | | |
| **A4: Không HB** | | | | | **X** | **X** | **X** | **X** |

> **Giải thích:**
> - R1 (T,T,T): Cả 3 đạt → A1 (Xuất sắc)
> - R2 (T,T,F): C1+C2 đạt, có KL → chỉ C1 đạt (vì KL ảnh hưởng) → A3 (Tiềm năng)
> - R3 (T,F,T): C1+C3 đạt, thiếu C2 → A2 (Khuyến khích)
> - R4 (T,F,F): Chỉ C1 đạt → A3 (Tiềm năng)
> - R5–R8: Không đạt C1 → A4 (Không học bổng)

---

### Bước 3: Bảng ca kiểm thử

| TC ID | GPA | Tín chỉ | Kỷ luật | Rule | Kết quả mong đợi |
|:--:|:--:|:--:|:--:|:--:|:--|
| **TC01** | 3.5 | 65 | Không có | R1 | Học bổng Xuất sắc – 100% học phí |
| **TC02** | 3.6 | 70 | Có cảnh cáo | R2 | Học bổng Tiềm năng – 20% học phí |
| **TC03** | 3.4 | 45 | Không có | R3 | Học bổng Khuyến khích – 50% học phí |
| **TC04** | 3.3 | 50 | Có cảnh cáo | R4 | Học bổng Tiềm năng – 20% học phí |
| **TC05** | 2.8 | 80 | Không có | R5 | Không được học bổng |
| **TC06** | 2.5 | 75 | Có cảnh cáo | R6 | Không được học bổng |
| **TC07** | 3.0 | 40 | Không có | R7 | Không được học bổng |
| **TC08** | 2.9 | 30 | Có cảnh cáo | R8 | Không được học bổng |

---

## CÂU 2 – LỜI GIẢI (4 điểm)

### Bước 1: Xác định các nút CFG

```
Nút 1: result = 0;
Nút 2: [IF] score>=5 || (attendance>=80 && passed==1) ?   ← điều kiện phức hợp
Nút 3: [IF] score >= 8 ?
Nút 4: result = 3;
Nút 5: [ELSE IF] score >= 6 ?
Nút 6: result = 2;
Nút 7: result = 1;
Nút 8: return result;
```

### Bước 2: Tính độ phức tạp Cyclomatic V(G)

- **Số nút (N):** 8
- **Số cung (E):** 11
  - 1→2, 2→3(True), 2→8(False), 3→4(True), 3→5(False), 4→8, 5→6(True), 5→7(False), 6→8, 7→8
- **Số nút vị từ (P):** 3 (Nút 2, Nút 3, Nút 5)

> **Công thức 1:** V(G) = E − N + 2 = 11 − 8 + 2 = **5**
>
> **Công thức 2:** V(G) = P + 1 = 3 + 1 = **4**

### Bước 3: Phân tích điều kiện cho Branch & Condition Coverage

Điều kiện tại Nút 2: `score>=5` **OR** `(attendance>=80 AND passed==1)`

Ký hiệu: A = `score>=5`, B = `attendance>=80`, C = `passed==1`

Để đạt **Bao phủ điều kiện (Condition Coverage)**: mỗi điều kiện đơn (A, B, C) phải có lần True và lần False.

### Bước 4: Bảng ca kiểm thử Branch & Condition Coverage

| TC ID | score | attendance | passed | A(s≥5) | B(att≥80) | C(passed=1) | Nút 2 | Kết quả (result) |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| **TC01** | 9 | 90 | 1 | T | T | T | True | 3 (Giỏi) – Nút 3 True |
| **TC02** | 7 | 70 | 1 | T | F | T | True | 2 (Khá) – Nút 3 False, Nút 5 True |
| **TC03** | 5 | 60 | 0 | T | F | F | True | 1 (TB) – Nút 3 F, Nút 5 F |
| **TC04** | 3 | 85 | 1 | F | T | T | True | 1 (TB) – A=F nhưng B&&C=T |
| **TC05** | 3 | 70 | 0 | F | F | F | False | 0 (Không đạt) |

> - TC01: Bao phủ A=T, B=T, C=T, nhánh Nút 2=True, Nút 3=True → result=3
> - TC02: A=T (đủ True nút 2), Nút 3=False, Nút 5=True → result=2
> - TC03: A=T, B=F (B có False), C=F (C có False), Nút 5=False → result=1
> - TC04: A=F (A có False), B=T, C=T (B&&C=True → vào khối if) → result=1
> - TC05: A=F, B=F → toàn bộ False, Nút 2=False → result=0

→ Tổng hợp: A có T(TC01,02,03) và F(TC04,05); B có T(TC01,04) và F(TC02,03,05); C có T(TC01,02,04) và F(TC03,05). Mọi điều kiện đơn đều có True và False → đạt Branch & Condition Coverage.

---

> **Tổng kết điểm:**
> - Câu 1 (Bảng quyết định): 6 điểm – Xác định đúng C và A (1đ), bảng đủ 8 rules (2đ), bảng TC đúng (3đ).
> - Câu 2 (Hộp trắng): 4 điểm – CFG đúng (1đ), V(G) đúng (1đ), phân tích điều kiện đúng (1đ), bảng TC đủ bao phủ (1đ).
