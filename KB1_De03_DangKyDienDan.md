# ĐỀ THI GIỮA KỲ – MÔN KIỂM THỬ PHẦN MỀM
## **ĐỀ 03 – KỊCH BẢN 1**
### Thời gian: 60 phút | Được sử dụng tài liệu: Không

---

## CÂU 1 (6 ĐIỂM) – KIỂM THỬ HỘP ĐEN (Black-box Testing)

### Đặc tả bài toán: Hệ thống đăng ký tài khoản diễn đàn trực tuyến

Một diễn đàn trực tuyến cho phép người dùng đăng ký tài khoản với các quy định sau:

- **Độ tuổi đăng ký hợp lệ:** Tối thiểu **13 tuổi**, tối đa **99 tuổi**. Người ngoài độ tuổi này không được đăng ký.
- **Tên đăng nhập (Username):** Độ dài từ **6 đến 20 ký tự**, chỉ gồm chữ cái, chữ số và dấu gạch dưới `_`. Không được bắt đầu bằng chữ số.
- **Phân loại thành viên** theo độ tuổi hợp lệ:

| Độ tuổi | Loại thành viên | Quyền hạn |
|:--|:--|:--|
| 13 – 17 tuổi | Thành viên Thiếu niên | Đọc bài, bình luận, không được tạo chủ đề |
| 18 – 60 tuổi | Thành viên Trưởng thành | Toàn quyền (đọc, bình luận, tạo chủ đề) |
| 61 – 99 tuổi | Thành viên Cao tuổi | Đọc bài, bình luận, không được tạo chủ đề |

---

### a. Áp dụng kỹ thuật Kiểm thử Lớp tương đương (3 điểm)

**Yêu cầu:**
1. Xác định các biến đầu vào và phân chia lớp tương đương hợp lệ / không hợp lệ cho từng biến.
2. Thiết kế bảng ca kiểm thử (Test Cases) tương ứng, đảm bảo mỗi lớp được bao phủ ít nhất một lần.

---

### b. Áp dụng kỹ thuật Kiểm thử Giá trị biên (3 điểm)

**Yêu cầu:**
1. Xác định các điểm biên cho biến **Độ tuổi** và biến **Độ dài tên đăng nhập**.
2. Thiết kế bảng ca kiểm thử (BVA Test Cases) cho tất cả các giá trị biên đã xác định.

---

## CÂU 2 (4 ĐIỂM) – KIỂM THỬ HỘP TRẮNG (White-box Testing)

### Mã nguồn:

```c
int GetMaxDay(int month, int year)
{
    int maxDay;
    if (month == 2)
    {
        if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0))
            maxDay = 29;
        else
            maxDay = 28;
    }
    else if (month == 4 || month == 6 || month == 9 || month == 11)
        maxDay = 30;
    else
        maxDay = 31;
    return maxDay;
}
```

**Yêu cầu:**
1. Vẽ Đồ thị luồng điều khiển (CFG) của hàm trên. Đánh số nút rõ ràng.
2. Tính độ phức tạp Cyclomatic V(G) bằng hai công thức khác nhau.
3. Liệt kê các đường thi hành độc lập (Basis Paths).
4. Thiết kế bảng ca kiểm thử tương ứng cho từng đường thi hành (ghi rõ Input, đường đi qua các nút, kết quả mong đợi).

---

### Hết

---
---

# LỜI GIẢI CHI TIẾT – ĐỀ 03 KỊCH BẢN 1

---

## CÂU 1 – LỜI GIẢI (6 điểm)

### Xác định biến đầu vào

| Biến | Ký hiệu | Miền giá trị hợp lệ |
|:--|:--|:--|
| Độ tuổi | A | 13 ≤ A ≤ 99 (số nguyên) |
| Tên đăng nhập | U | Chuỗi 6–20 ký tự, gồm [a-z, A-Z, 0-9, _], không bắt đầu bằng số |

---

### a. Kiểm thử Lớp tương đương (3 điểm)

#### Bước 1: Phân chia lớp tương đương

| Biến | Lớp hợp lệ | Lớp không hợp lệ |
|:--|:--|:--|
| Độ tuổi (A) | **EC1:** 13 ≤ A ≤ 17 → Thiếu niên | **EC7:** A < 13 |
| | **EC2:** 18 ≤ A ≤ 60 → Trưởng thành | **EC8:** A > 99 |
| | **EC3:** 61 ≤ A ≤ 99 → Cao tuổi | **EC9:** A không phải số nguyên |
| Username (U) | **EC4:** Dài 6–20 ký tự, ký tự hợp lệ, không bắt đầu bằng số | **EC10:** Dài < 6 ký tự |
| | | **EC11:** Dài > 20 ký tự |
| | | **EC12:** Chứa ký tự đặc biệt (không phải _, a-z, 0-9) |
| | | **EC13:** Bắt đầu bằng chữ số |

#### Bước 2: Bảng ca kiểm thử Lớp tương đương

| TC ID | Mục đích | Tuổi (A) | Username (U) | Lớp bao phủ | Kết quả mong đợi |
|:--:|:--|:--:|:--:|:--:|:--|
| **TC01** | Đăng ký thành viên Thiếu niên | 15 | user_abc | EC1, EC4 | Thành công. Loại: Thiếu niên |
| **TC02** | Đăng ký thành viên Trưởng thành | 25 | user_abc | EC2, EC4 | Thành công. Loại: Trưởng thành |
| **TC03** | Đăng ký thành viên Cao tuổi | 70 | user_abc | EC3, EC4 | Thành công. Loại: Cao tuổi |
| **TC04** | Tuổi dưới 13 | 10 | user_abc | EC7, EC4 | Lỗi: Độ tuổi tối thiểu là 13 |
| **TC05** | Tuổi trên 99 | 105 | user_abc | EC8, EC4 | Lỗi: Độ tuổi tối đa là 99 |
| **TC06** | Tuổi không phải số | "abc" | user_abc | EC9, EC4 | Lỗi: Tuổi phải là số nguyên |
| **TC07** | Username quá ngắn (< 6 ký tự) | 25 | abc | EC2, EC10 | Lỗi: Username tối thiểu 6 ký tự |
| **TC08** | Username quá dài (> 20 ký tự) | 25 | abcdefghijklmnopqrstu | EC2, EC11 | Lỗi: Username tối đa 20 ký tự |
| **TC09** | Username chứa ký tự đặc biệt | 25 | user@name | EC2, EC12 | Lỗi: Ký tự không hợp lệ trong username |
| **TC10** | Username bắt đầu bằng số | 25 | 1username | EC2, EC13 | Lỗi: Username không được bắt đầu bằng số |

---

### b. Kiểm thử Giá trị biên (3 điểm)

#### Bước 1: Xác định điểm biên

- **Biến Độ tuổi (A):** Miền [13, 99], điểm phân chia tại 17/18 và 60/61.
  - Biên tại 13: {12, 13, 14}
  - Biên phân chia 17/18: {16, 17, 18}
  - Biên phân chia 60/61: {59, 60, 61}
  - Biên tại 99: {98, 99, 100}

- **Biến Độ dài Username (L):** Miền [6, 20].
  - Biên tại 6: {5, 6, 7}
  - Biên tại 20: {19, 20, 21}

#### Bước 2: Bảng ca kiểm thử Giá trị biên

**Biên Độ tuổi** (dùng username hợp lệ cố định: `user_ok`):

| TC ID | Mô tả | Tuổi (A) | Kết quả mong đợi |
|:--:|:--|:--:|:--|
| **BVA01** | Dưới biên tối thiểu tuổi | 12 | Lỗi: Không đủ tuổi đăng ký |
| **BVA02** | Biên tối thiểu tuổi | 13 | Thành công. Loại: Thiếu niên |
| **BVA03** | Ngay trên biên tối thiểu | 14 | Thành công. Loại: Thiếu niên |
| **BVA04** | Ngay dưới biên phân chia 17/18 | 16 | Thành công. Loại: Thiếu niên |
| **BVA05** | Biên trên Thiếu niên | 17 | Thành công. Loại: Thiếu niên |
| **BVA06** | Biên dưới Trưởng thành | 18 | Thành công. Loại: Trưởng thành |
| **BVA07** | Ngay dưới biên phân chia 60/61 | 59 | Thành công. Loại: Trưởng thành |
| **BVA08** | Biên trên Trưởng thành | 60 | Thành công. Loại: Trưởng thành |
| **BVA09** | Biên dưới Cao tuổi | 61 | Thành công. Loại: Cao tuổi |
| **BVA10** | Ngay dưới biên tối đa tuổi | 98 | Thành công. Loại: Cao tuổi |
| **BVA11** | Biên tối đa tuổi | 99 | Thành công. Loại: Cao tuổi |
| **BVA12** | Vượt biên tối đa tuổi | 100 | Lỗi: Độ tuổi vượt quá giới hạn |

**Biên Độ dài Username** (dùng tuổi hợp lệ cố định: 25):

| TC ID | Mô tả | Độ dài Username | Kết quả mong đợi |
|:--:|:--|:--:|:--|
| **BVA13** | Dưới biên tối thiểu username | 5 (vd: `user1`) | Lỗi: Username tối thiểu 6 ký tự |
| **BVA14** | Biên tối thiểu username | 6 (vd: `user12`) | Thành công |
| **BVA15** | Ngay trên biên tối thiểu | 7 (vd: `user123`) | Thành công |
| **BVA16** | Ngay dưới biên tối đa username | 19 | Thành công |
| **BVA17** | Biên tối đa username | 20 | Thành công |
| **BVA18** | Vượt biên tối đa username | 21 | Lỗi: Username tối đa 20 ký tự |

---

## CÂU 2 – LỜI GIẢI (4 điểm)

### Bước 1: Đánh số câu lệnh và xác định các nút CFG

```
Nút 1: (Vào hàm – khai báo maxDay)
Nút 2: [IF] month == 2 ?
Nút 3: [IF] năm nhuận: (year%4==0 && year%100!=0) || (year%400==0) ?
Nút 4: maxDay = 29;
Nút 5: maxDay = 28;
Nút 6: [ELSE IF] month == 4 || 6 || 9 || 11 ?
Nút 7: maxDay = 30;
Nút 8: maxDay = 31;
Nút 9: return maxDay;
```

### Bước 2: Tính độ phức tạp Cyclomatic V(G)

- **Số nút (N):** 9
- **Số cung (E):** 11
  - 1→2, 2→3(True), 2→6(False), 3→4(True), 3→5(False), 4→9, 5→9, 6→7(True), 6→8(False), 7→9, 8→9
- **Số nút vị từ (P):** 3 (Nút 2, Nút 3, Nút 6)

> **Công thức 1:** V(G) = E − N + 2 = 11 − 9 + 2 = **4**
>
> **Công thức 2:** V(G) = P + 1 = 3 + 1 = **4**

→ Cần **4 đường thi hành cơ sở**.

### Bước 3: Liệt kê các đường thi hành cơ sở (Basis Paths)

| STT | Đường thi hành | Mô tả |
|:--:|:--|:--|
| **P1** | 1 → 2(True) → 3(True) → 4 → 9 | Tháng 2, năm nhuận → 29 ngày |
| **P2** | 1 → 2(True) → 3(False) → 5 → 9 | Tháng 2, không nhuận → 28 ngày |
| **P3** | 1 → 2(False) → 6(True) → 7 → 9 | Tháng 4/6/9/11 → 30 ngày |
| **P4** | 1 → 2(False) → 6(False) → 8 → 9 | Các tháng còn lại (1,3,5,7,8,10,12) → 31 ngày |

### Bước 4: Bảng ca kiểm thử

| TC ID | Input (month, year) | Đường đi | Kết quả mong đợi (maxDay) |
|:--:|:--:|:--|:--:|
| **TC_P1** | month=2, year=2024 | 1→2(T)→3(T)→4→9 | 29 (2024 là năm nhuận: 2024%4=0, 2024%100≠0) |
| **TC_P2** | month=2, year=2023 | 1→2(T)→3(F)→5→9 | 28 (2023 không nhuận) |
| **TC_P3** | month=4, year=2024 | 1→2(F)→6(T)→7→9 | 30 (tháng 4 có 30 ngày) |
| **TC_P4** | month=1, year=2024 | 1→2(F)→6(F)→8→9 | 31 (tháng 1 có 31 ngày) |

---

> **Tổng kết điểm:**
> - Câu 1a (Lớp tương đương): 3 điểm – Đủ 2 biến, đủ lớp, bảng TC ≥ 1 TC/lớp.
> - Câu 1b (Giá trị biên): 3 điểm – Đủ 4 cụm biên tuổi + 2 cụm biên username.
> - Câu 2 (Hộp trắng): 4 điểm – CFG đúng (1đ), V(G) = 4 bằng 2 CT (1đ), đủ 4 Basis Paths (1đ), bảng TC đúng (1đ).
