# ĐỀ THI GIỮA KỲ – MÔN KIỂM THỬ PHẦN MỀM
## **ĐỀ 03 – KỊCH BẢN 2**
### Thời gian: 60 phút | Được sử dụng tài liệu: Không

---

## CÂU 1 (6 ĐIỂM) – KIỂM THỬ HỘP ĐEN (Black-box Testing)

### Đặc tả bài toán: Hệ thống xét hạn mức tín dụng ngân hàng

Một ngân hàng xét duyệt hạn mức thẻ tín dụng dựa trên **ba tiêu chí** sau:

- **C1 – Thu nhập hàng tháng:** Từ **15 triệu VNĐ** trở lên được coi là đạt yêu cầu.
- **C2 – Lịch sử tín dụng:** Không có nợ xấu trong vòng 12 tháng gần nhất (Tốt / Có nợ xấu).
- **C3 – Thời gian làm việc tại đơn vị hiện tại:** Từ **12 tháng** trở lên (Ổn định / Chưa ổn định).

**Các mức hạn mức tín dụng được duyệt:**

| Điều kiện thỏa mãn | Hạn mức tín dụng |
|:--|:--|
| Đủ cả 3 điều kiện (C1, C2, C3) | 50.000.000 VNĐ |
| Đạt C1 và C2 (thiếu C3) | 30.000.000 VNĐ |
| Đạt C1 và C3 (thiếu C2) | 20.000.000 VNĐ |
| Chỉ đạt C1 (thiếu C2 và C3) | 10.000.000 VNĐ |
| Không đạt C1 (dù C2, C3 thế nào) | Từ chối – Không duyệt thẻ |

---

### Áp dụng kỹ thuật Kiểm thử Bảng quyết định (Decision Table Testing) (6 điểm)

**Yêu cầu:**
1. Xác định các điều kiện (Conditions) và hành động (Actions) của bài toán.
2. Xây dựng **Bảng quyết định (Decision Table)** đầy đủ với tất cả các tổ hợp điều kiện có thể. Gộp các tổ hợp có cùng kết quả nếu có thể.
3. Thiết kế **ca kiểm thử (Test Cases)** tương ứng cho mỗi quy tắc (rule) trong bảng quyết định. Ghi rõ: Mã TC, dữ liệu đầu vào (Thu nhập, Lịch sử tín dụng, Thời gian làm việc), kết quả mong đợi (Hạn mức được duyệt).

---

## CÂU 2 (4 ĐIỂM) – KIỂM THỬ HỘP TRẮNG (White-box Testing)

### Mã nguồn:

```c
int checkLogin(char* username, char* password, int isAdmin)
{
    int status = 0;
    if (username != NULL && password != NULL)
    {
        if (strlen(password) >= 8)
        {
            status = 1;
            if (isAdmin == 1)
                status = 2;
        }
    }
    return status;
}
```

> **Chú thích:** Trả về: 0 = Thất bại, 1 = Thành công (user thường), 2 = Thành công (admin).

**Yêu cầu:**
1. Vẽ Đồ thị luồng điều khiển (CFG) của hàm trên. Đánh số nút rõ ràng.
2. Tính độ phức tạp Cyclomatic V(G) bằng hai công thức khác nhau.
3. Liệt kê tất cả các **câu lệnh** và **quyết định (nhánh)** trong hàm.
4. Thiết kế bảng ca kiểm thử thỏa mãn đồng thời hai tiêu chí **Bao phủ câu lệnh (Statement Coverage)** và **Bao phủ quyết định (Decision Coverage)**. Ghi rõ: Mã TC, dữ liệu đầu vào, các câu lệnh/nhánh được bao phủ, kết quả mong đợi.

---

### Hết

---
---

# LỜI GIẢI CHI TIẾT – ĐỀ 03 KỊCH BẢN 2

---

## CÂU 1 – LỜI GIẢI (6 điểm)

### Bước 1: Xác định Điều kiện và Hành động

**Các điều kiện (Conditions):**

| Ký hiệu | Điều kiện |
|:--:|:--|
| **C1** | Thu nhập ≥ 15 triệu (T/F) |
| **C2** | Không có nợ xấu (T/F) |
| **C3** | Làm việc ≥ 12 tháng (T/F) |

**Các hành động (Actions):**

| Ký hiệu | Hành động |
|:--:|:--|
| **A1** | Hạn mức 50.000.000 VNĐ |
| **A2** | Hạn mức 30.000.000 VNĐ |
| **A3** | Hạn mức 20.000.000 VNĐ |
| **A4** | Hạn mức 10.000.000 VNĐ |
| **A5** | Từ chối – Không duyệt thẻ |

---

### Bước 2: Bảng quyết định (Decision Table)

3 điều kiện nhị phân → 2³ = 8 tổ hợp. Phân tích:

| Điều kiện / Hành động | R1 | R2 | R3 | R4 | R5–R8 (gộp) |
|:--|:--:|:--:|:--:|:--:|:--:|
| **C1: TN ≥ 15tr** | T | T | T | T | F |
| **C2: Không nợ xấu** | T | T | F | F | * |
| **C3: Làm việc ≥ 12th** | T | F | T | F | * |
| **A1: 50 triệu** | **X** | | | | |
| **A2: 30 triệu** | | **X** | | | |
| **A3: 20 triệu** | | | **X** | | |
| **A4: 10 triệu** | | | | **X** | |
| **A5: Từ chối** | | | | | **X** |

> **Ghi chú:** R5–R8 (C1=F, bất kể C2, C3) → đều từ chối. Gộp thành 1 cột đại diện.

**Bảng đầy đủ 8 rules:**

| | R1 | R2 | R3 | R4 | R5 | R6 | R7 | R8 |
|:--|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| **C1** | T | T | T | T | F | F | F | F |
| **C2** | T | T | F | F | T | T | F | F |
| **C3** | T | F | T | F | T | F | T | F |
| **A1: 50tr** | **X** | | | | | | | |
| **A2: 30tr** | | **X** | | | | | | |
| **A3: 20tr** | | | **X** | | | | | |
| **A4: 10tr** | | | | **X** | | | | |
| **A5: Từ chối** | | | | | **X** | **X** | **X** | **X** |

---

### Bước 3: Bảng ca kiểm thử

| TC ID | Thu nhập (tr/th) | Lịch sử tín dụng | Thời gian làm việc | Rule | Kết quả mong đợi |
|:--:|:--:|:--:|:--:|:--:|:--|
| **TC01** | 20 triệu | Không nợ xấu | 24 tháng | R1 | Hạn mức: **50.000.000 VNĐ** |
| **TC02** | 18 triệu | Không nợ xấu | 8 tháng | R2 | Hạn mức: **30.000.000 VNĐ** |
| **TC03** | 16 triệu | Có nợ xấu | 18 tháng | R3 | Hạn mức: **20.000.000 VNĐ** |
| **TC04** | 15 triệu | Có nợ xấu | 6 tháng | R4 | Hạn mức: **10.000.000 VNĐ** |
| **TC05** | 10 triệu | Không nợ xấu | 24 tháng | R5 | **Từ chối** – Không đủ thu nhập |
| **TC06** | 12 triệu | Không nợ xấu | 5 tháng | R6 | **Từ chối** – Không đủ thu nhập |
| **TC07** | 8 triệu | Có nợ xấu | 20 tháng | R7 | **Từ chối** – Không đủ thu nhập |
| **TC08** | 5 triệu | Có nợ xấu | 3 tháng | R8 | **Từ chối** – Không đủ thu nhập |

---

## CÂU 2 – LỜI GIẢI (4 điểm)

### Bước 1: Đánh số câu lệnh và xác định nút CFG

```
Nút 1: status = 0;
Nút 2: [IF] username != NULL && password != NULL ?   ← Điều kiện ngoài
Nút 3: [IF] strlen(password) >= 8 ?                 ← Điều kiện giữa
Nút 4: status = 1;
Nút 5: [IF] isAdmin == 1 ?                          ← Điều kiện trong
Nút 6: status = 2;
Nút 7: return status;
```

### Bước 2: Tính độ phức tạp Cyclomatic V(G)

- **Số nút (N):** 7
- **Số cung (E):** 9
  - 1→2, 2→3(True), 2→7(False), 3→4(True), 3→7(False), 4→5, 5→6(True), 5→7(False), 6→7
- **Số nút vị từ (P):** 3 (Nút 2, Nút 3, Nút 5)

> **Công thức 1:** V(G) = E − N + 2 = 9 − 7 + 2 = **4**
>
> **Công thức 2:** V(G) = P + 1 = 3 + 1 = **4**

### Bước 3: Liệt kê tất cả câu lệnh và quyết định

**Danh sách câu lệnh (Statements):**

| STT | Câu lệnh |
|:--:|:--|
| S1 | `status = 0` |
| S2 | Kiểm tra `username != NULL && password != NULL` |
| S3 | Kiểm tra `strlen(password) >= 8` |
| S4 | `status = 1` |
| S5 | Kiểm tra `isAdmin == 1` |
| S6 | `status = 2` |
| S7 | `return status` |

**Danh sách quyết định/nhánh (Decisions/Branches):**

| QĐ | Điều kiện | Nhánh True | Nhánh False |
|:--:|:--|:--|:--|
| D1 | `username!=NULL && password!=NULL` | Vào khối if ngoài | Bỏ qua, về return |
| D2 | `strlen(password) >= 8` | Vào khối if giữa | Bỏ qua, về return |
| D3 | `isAdmin == 1` | status = 2 | Giữ status = 1, về return |

---

### Bước 4: Bảng ca kiểm thử – Statement + Decision Coverage

**Tiêu chí Statement Coverage:** Mọi câu lệnh (S1–S7) phải thực thi ít nhất 1 lần.

**Tiêu chí Decision Coverage:** Mọi nhánh True/False của D1, D2, D3 phải thực thi ít nhất 1 lần.

| TC ID | username | password | isAdmin | D1 | D2 | D3 | Câu lệnh thực thi | status (KQ) |
|:--:|:--|:--|:--:|:--:|:--:|:--:|:--|:--:|
| **TC01** | "admin" | "pass12345" | 1 | T | T | T | S1,S2,S3,S4,S5,S6,S7 | **2** (Admin) |
| **TC02** | "user1" | "pass12345" | 0 | T | T | F | S1,S2,S3,S4,S5,S7 | **1** (User) |
| **TC03** | "user1" | "abc" | 0 | T | F | - | S1,S2,S3,S7 | **0** (Thất bại – pass ngắn) |
| **TC04** | NULL | NULL | 0 | F | - | - | S1,S2,S7 | **0** (Thất bại – null) |

**Kiểm tra bao phủ:**

| Nhánh | Được bao phủ bởi |
|:--|:--|
| D1 = True | TC01, TC02, TC03 |
| D1 = False | TC04 |
| D2 = True | TC01, TC02 |
| D2 = False | TC03 |
| D3 = True | TC01 |
| D3 = False | TC02 |

✅ **Statement Coverage:** S1–S7 đều được thực thi (TC01 bao phủ toàn bộ đường dài nhất).

✅ **Decision Coverage:** Mọi nhánh T/F của D1, D2, D3 đều có test case bao phủ.

---

> **Tổng kết điểm:**
> - Câu 1 (Bảng quyết định): 6 điểm – Xác định đúng C và A (1đ), bảng đủ 8 rules (2đ), bảng TC đúng (3đ).
> - Câu 2 (Hộp trắng – Stmt+Decision): 4 điểm – CFG đúng (1đ), V(G)=4 bằng 2 CT (1đ), liệt kê đúng S và D (0.5đ), bảng TC đạt cả 2 tiêu chí (1.5đ).
