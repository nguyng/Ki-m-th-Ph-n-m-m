# ĐỀ THI GIỮA KỲ – MÔN KIỂM THỬ PHẦN MỀM
## **ĐỀ 02 – KỊCH BẢN 1**
### Thời gian: 60 phút | Được sử dụng tài liệu: Không

---

## CÂU 1 (6 ĐIỂM) – KIỂM THỬ HỘP ĐEN (Black-box Testing)

### Đặc tả bài toán: Hệ thống tính phí giao dịch ngân hàng trực tuyến

Một ngân hàng áp dụng quy tắc tính phí giao dịch chuyển tiền trực tuyến như sau:

- **Số tiền giao dịch hợp lệ:** Tối thiểu **10.000 VNĐ**, tối đa **500.000.000 VNĐ**.
- Nếu số tiền nằm ngoài phạm vi trên → Hệ thống từ chối và báo lỗi.
- Nếu hợp lệ → Hệ thống tính phí theo bảng sau:

| Số tiền giao dịch | Phí giao dịch |
|:--|:--|
| 10.000 đến dưới 1.000.000 VNĐ | 5.000 VNĐ (cố định) |
| 1.000.000 đến 10.000.000 VNĐ | 10.000 VNĐ (cố định) |
| Trên 10.000.000 VNĐ | 0,1% số tiền giao dịch |

- **Số tài khoản nhận:** Phải là chuỗi số gồm đúng **10 hoặc 14 chữ số** (không chứa chữ cái hay ký tự đặc biệt).

---

### a. Áp dụng kỹ thuật Kiểm thử Lớp tương đương (3 điểm)

**Yêu cầu:**
1. Xác định các biến đầu vào và phân chia lớp tương đương hợp lệ / không hợp lệ cho từng biến.
2. Thiết kế bảng ca kiểm thử (Test Cases) tương ứng, đảm bảo mỗi lớp được bao phủ ít nhất một lần.

---

### b. Áp dụng kỹ thuật Kiểm thử Giá trị biên (3 điểm)

**Yêu cầu:**
1. Xác định các điểm biên cho biến **Số tiền giao dịch**.
2. Thiết kế bảng ca kiểm thử (BVA Test Cases) cho tất cả các giá trị biên đã xác định.

---

## CÂU 2 (4 ĐIỂM) – KIỂM THỬ HỘP TRẮNG (White-box Testing)

### Mã nguồn:

```c
int check_d_after_e(char s[])
{
    int i = 0;
    int kq = 0;
    while (s[i] != '\0')
    {
        if (s[i] == 'e')
        {
            i++;
            if (s[i] == 'd')
                kq = 1;
        }
        i++;
    }
    return kq;
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

# LỜI GIẢI CHI TIẾT – ĐỀ 02 KỊCH BẢN 1

---

## CÂU 1 – LỜI GIẢI (6 điểm)

### Xác định biến đầu vào

| Biến | Ký hiệu | Miền giá trị hợp lệ |
|:--|:--|:--|
| Số tiền giao dịch | T | 10.000 ≤ T ≤ 500.000.000 (VNĐ, số nguyên dương) |
| Số tài khoản nhận | STK | Chuỗi số nguyên, độ dài đúng 10 hoặc 14 ký tự |

---

### a. Kiểm thử Lớp tương đương (3 điểm)

#### Bước 1: Phân chia lớp tương đương

| Biến đầu vào | Lớp hợp lệ | Lớp không hợp lệ |
|:--|:--|:--|
| Số tiền (T) | **EC1:** 10.000 ≤ T < 1.000.000 → phí 5.000 VNĐ | **EC6:** T < 10.000 |
| | **EC2:** 1.000.000 ≤ T ≤ 10.000.000 → phí 10.000 VNĐ | **EC7:** T > 500.000.000 |
| | **EC3:** T > 10.000.000 → phí 0,1% | **EC8:** T không phải số (chữ, ký tự đặc biệt) |
| Số tài khoản (STK) | **EC4:** Đúng 10 chữ số | **EC9:** Độ dài khác 10 và 14 (vd: 9, 11, 13 số) |
| | **EC5:** Đúng 14 chữ số | **EC10:** Chứa chữ cái hoặc ký tự đặc biệt |

#### Bước 2: Bảng ca kiểm thử Lớp tương đương

| TC ID | Mục đích | Số tiền (T) | Số TK | Lớp bao phủ | Kết quả mong đợi |
|:--:|:--|:--:|:--:|:--:|:--|
| **TC01** | Phí cố định 5.000đ | 500.000 | 0123456789 | EC1, EC4 | Thành công. Phí: 5.000 VNĐ |
| **TC02** | Phí cố định 10.000đ | 5.000.000 | 0123456789 | EC2, EC4 | Thành công. Phí: 10.000 VNĐ |
| **TC03** | Phí 0,1% | 50.000.000 | 01234567890123 | EC3, EC5 | Thành công. Phí: 50.000 VNĐ |
| **TC04** | STK 14 chữ số hợp lệ | 500.000 | 01234567890123 | EC1, EC5 | Thành công. Phí: 5.000 VNĐ |
| **TC05** | Số tiền quá nhỏ | 5.000 | 0123456789 | EC6 | Lỗi: Số tiền tối thiểu 10.000 VNĐ |
| **TC06** | Số tiền quá lớn | 600.000.000 | 0123456789 | EC7 | Lỗi: Số tiền vượt hạn mức |
| **TC07** | Số tiền không phải số | "abc" | 0123456789 | EC8 | Lỗi: Số tiền không hợp lệ |
| **TC08** | STK sai độ dài (9 số) | 500.000 | 012345678 | EC1, EC9 | Lỗi: Số tài khoản không hợp lệ |
| **TC09** | STK chứa chữ cái | 500.000 | 012345678A | EC1, EC10 | Lỗi: Số tài khoản chứa ký tự sai |

---

### b. Kiểm thử Giá trị biên (3 điểm)

#### Bước 1: Xác định các điểm biên của Số tiền (T)

- Biên tối thiểu: 10.000 → {9.999; 10.000; 10.001}
- Biên phân chia lớp 1/2 tại 1.000.000: {999.999; 1.000.000; 1.000.001}
- Biên phân chia lớp 2/3 tại 10.000.000: {9.999.999; 10.000.000; 10.000.001}
- Biên tối đa: 500.000.000 → {499.999.999; 500.000.000; 500.000.001}

#### Bước 2: Bảng ca kiểm thử Giá trị biên (dùng STK hợp lệ cố định: 0123456789)

| TC ID | Mô tả | Số tiền (T) | Kết quả mong đợi |
|:--:|:--|--:|:--|
| **BVA01** | Dưới biên tối thiểu | 9.999 | Lỗi: Số tiền tối thiểu 10.000 VNĐ |
| **BVA02** | Tại biên tối thiểu | 10.000 | Thành công. Phí: 5.000 VNĐ |
| **BVA03** | Ngay trên biên tối thiểu | 10.001 | Thành công. Phí: 5.000 VNĐ |
| **BVA04** | Ngay dưới biên phân chia 1tr | 999.999 | Thành công. Phí: 5.000 VNĐ |
| **BVA05** | Tại biên 1.000.000 | 1.000.000 | Thành công. Phí: 10.000 VNĐ |
| **BVA06** | Ngay trên biên 1.000.000 | 1.000.001 | Thành công. Phí: 10.000 VNĐ |
| **BVA07** | Ngay dưới biên phân chia 10tr | 9.999.999 | Thành công. Phí: 10.000 VNĐ |
| **BVA08** | Tại biên 10.000.000 | 10.000.000 | Thành công. Phí: 10.000 VNĐ |
| **BVA09** | Ngay trên biên 10.000.000 | 10.000.001 | Thành công. Phí: 10.001 VNĐ (0,1%) |
| **BVA10** | Ngay dưới biên tối đa | 499.999.999 | Thành công. Phí: 499.999 VNĐ (0,1%) |
| **BVA11** | Tại biên tối đa | 500.000.000 | Thành công. Phí: 500.000 VNĐ (0,1%) |
| **BVA12** | Vượt biên tối đa | 500.000.001 | Lỗi: Số tiền vượt hạn mức cho phép |

---

## CÂU 2 – LỜI GIẢI (4 điểm)

### Bước 1: Đánh số câu lệnh và xác định các nút CFG

```
Nút 1: i = 0; kq = 0;
Nút 2: [WHILE] s[i] != '\0' ?           ← điều kiện vòng lặp ngoài
Nút 3: [IF] s[i] == 'e' ?               ← kiểm tra ký tự 'e'
Nút 4: i++;                             ← tăng i bên trong if
Nút 5: [IF] s[i] == 'd' ?              ← kiểm tra ký tự 'd'
Nút 6: kq = 1;
Nút 7: i++;                             ← tăng i cuối vòng lặp
Nút 8: return kq;
```

### Bước 2: Tính độ phức tạp Cyclomatic V(G)

- **Số nút (N):** 8
- **Số cung (E):** 11
  - 1→2, 2→3(True), 2→8(False), 3→4(True), 3→7(False), 4→5, 5→6(True), 5→7(False), 6→7, 7→2, 8 (kết thúc)
- **Số nút vị từ (P):** 3 (Nút 2, Nút 3, Nút 5)

> **Công thức 1:** V(G) = E − N + 2 = 11 − 8 + 2 = **5**
>
> **Công thức 2:** V(G) = P + 1 = 3 + 1 = **4**

→ Cần **4 đường thi hành cơ sở**.

### Bước 3: Liệt kê các đường thi hành cơ sở (Basis Paths)

| STT | Đường thi hành | Mô tả |
|:--:|:--|:--|
| **P1** | 1 → 2(False) → 8 | Chuỗi rỗng, không vào vòng lặp |
| **P2** | 1 → 2(True) → 3(False) → 7 → 2(False) → 8 | Ký tự không phải 'e', thoát vòng lặp |
| **P3** | 1 → 2(True) → 3(True) → 4 → 5(False) → 7 → 2(False) → 8 | Gặp 'e' nhưng sau không phải 'd' |
| **P4** | 1 → 2(True) → 3(True) → 4 → 5(True) → 6 → 7 → 2(False) → 8 | Gặp chuỗi 'ed', kq = 1 |

### Bước 4: Bảng ca kiểm thử

| TC ID | Input s[] | Đường đi | Kết quả mong đợi (kq) |
|:--:|:--|:--|:--:|
| **TC_P1** | `""` (chuỗi rỗng) | 1→2(F)→8 | 0 |
| **TC_P2** | `"abc"` (không có 'e') | 1→2(T)→3(F)→7→2(F)→8 | 0 |
| **TC_P3** | `"ex"` ('e' có, 'd' không có sau) | 1→2(T)→3(T)→4→5(F)→7→2(F)→8 | 0 |
| **TC_P4** | `"ed"` ('e' liền sau là 'd') | 1→2(T)→3(T)→4→5(T)→6→7→2(F)→8 | 1 |

---

> **Tổng kết điểm:**
> - Câu 1a (Lớp tương đương): 3 điểm – Đủ 2 biến, đủ lớp hợp lệ/không hợp lệ, bảng TC đầy đủ.
> - Câu 1b (Giá trị biên): 3 điểm – Xác định đúng 4 cụm biên, bảng BVA đủ 12 TC.
> - Câu 2 (Hộp trắng): 4 điểm – CFG đúng (1đ), V(G) đúng 2 CT (1đ), đủ Basis Paths (1đ), bảng TC đúng (1đ).
