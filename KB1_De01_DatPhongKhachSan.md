# ĐỀ THI GIỮA KỲ – MÔN KIỂM THỬ PHẦN MỀM
## **ĐỀ 01 – KỊCH BẢN 1**
### Thời gian: 60 phút | Được sử dụng tài liệu: Không

---

## CÂU 1 (6 ĐIỂM) – KIỂM THỬ HỘP ĐEN (Black-box Testing)

### Đặc tả bài toán: Hệ thống đặt phòng khách sạn trực tuyến

Một hệ thống đặt phòng khách sạn trực tuyến nhận đặt phòng dựa trên các quy tắc sau:

- **Số đêm lưu trú:** Tối thiểu **1 đêm**, tối đa **30 đêm**.
- **Số lượng khách:** Tối thiểu **1 người**, tối đa **4 người**.
- Nếu số đêm hoặc số khách nằm ngoài phạm vi trên → Hệ thống báo lỗi và từ chối đặt phòng.
- Nếu cả hai hợp lệ → Hệ thống xác nhận đặt phòng thành công và tính tổng chi phí theo bảng giá:

| Số đêm lưu trú | Giá mỗi đêm (VNĐ/phòng) |
|:-:|:-:|
| 1 – 7 đêm | 500.000 |
| 8 – 20 đêm | 450.000 |
| 21 – 30 đêm | 400.000 |

> **Ghi chú:** Mỗi phòng tối đa 4 khách. Chỉ đặt 1 phòng duy nhất.

---

### a. Áp dụng kỹ thuật Kiểm thử Lớp tương đương (3 điểm)

**Yêu cầu:**
1. Xác định các biến đầu vào và phân chia lớp tương đương hợp lệ / không hợp lệ.
2. Thiết kế bảng ca kiểm thử (Test Cases) tương ứng, đảm bảo mỗi lớp được bao phủ ít nhất một lần.

---

### b. Áp dụng kỹ thuật Kiểm thử Giá trị biên (3 điểm)

**Yêu cầu:**
1. Xác định các điểm biên cho từng biến đầu vào.
2. Thiết kế bảng ca kiểm thử (BVA Test Cases) cho tất cả các giá trị biên.

---

## CÂU 2 (4 ĐIỂM) – KIỂM THỬ HỘP TRẮNG (White-box Testing)

### Mã nguồn:

```c
int BinSearch(int X, int V[], int n)
{
    int low, high, mid;
    low = 0;
    high = n - 1;
    while (low <= high)
    {
        mid = (low + high) / 2;
        if (X < V[mid])
            high = mid - 1;
        else if (X > V[mid])
            low = mid + 1;
        else
            return mid;
    }
    return -1;
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

# LỜI GIẢI CHI TIẾT – ĐỀ 01 KỊCH BẢN 1

---

## CÂU 1 – LỜI GIẢI (6 điểm)

### Xác định biến đầu vào

| Biến | Ký hiệu | Miền giá trị hợp lệ |
|:--|:--|:--|
| Số đêm lưu trú | D | 1 ≤ D ≤ 30 (số nguyên dương) |
| Số lượng khách | K | 1 ≤ K ≤ 4 (số nguyên dương) |

---

### a. Kiểm thử Lớp tương đương (3 điểm)

#### Bước 1: Phân chia lớp tương đương

| Biến đầu vào | Lớp tương đương hợp lệ | Lớp tương đương không hợp lệ |
|:--|:--|:--|
| Số đêm (D) | **EC1:** 1 ≤ D ≤ 7 (giá 500.000/đêm) | **EC5:** D < 1 (số đêm âm hoặc bằng 0) |
| | **EC2:** 8 ≤ D ≤ 20 (giá 450.000/đêm) | **EC6:** D > 30 (quá giới hạn) |
| | **EC3:** 21 ≤ D ≤ 30 (giá 400.000/đêm) | **EC7:** D không phải số nguyên (ký tự, chữ) |
| Số khách (K) | **EC4:** 1 ≤ K ≤ 4 | **EC8:** K < 1 |
| | | **EC9:** K > 4 |
| | | **EC10:** K không phải số nguyên |

#### Bước 2: Bảng ca kiểm thử Lớp tương đương

| TC ID | Mục đích | Số đêm (D) | Số khách (K) | Lớp bao phủ | Kết quả mong đợi |
|:--:|:--|:--:|:--:|:--:|:--|
| **TC01** | Đặt phòng ngắn hạn (1–7 đêm) | 3 | 2 | EC1, EC4 | Thành công. Chi phí: 3 × 500.000 = 1.500.000 VNĐ |
| **TC02** | Đặt phòng trung hạn (8–20 đêm) | 10 | 1 | EC2, EC4 | Thành công. Chi phí: 10 × 450.000 = 4.500.000 VNĐ |
| **TC03** | Đặt phòng dài hạn (21–30 đêm) | 25 | 3 | EC3, EC4 | Thành công. Chi phí: 25 × 400.000 = 10.000.000 VNĐ |
| **TC04** | Số đêm bằng 0 (không hợp lệ) | 0 | 2 | EC5, EC4 | Báo lỗi: "Số đêm tối thiểu là 1" |
| **TC05** | Số đêm âm (không hợp lệ) | -5 | 2 | EC5, EC4 | Báo lỗi: "Số đêm không hợp lệ" |
| **TC06** | Số đêm vượt quá 30 | 35 | 2 | EC6, EC4 | Báo lỗi: "Số đêm tối đa là 30" |
| **TC07** | Số đêm là ký tự chữ | "abc" | 2 | EC7, EC4 | Báo lỗi: "Vui lòng nhập số nguyên" |
| **TC08** | Số khách bằng 0 | 5 | 0 | EC1, EC8 | Báo lỗi: "Số khách tối thiểu là 1" |
| **TC09** | Số khách vượt quá 4 | 5 | 6 | EC1, EC9 | Báo lỗi: "Số khách tối đa là 4" |
| **TC10** | Số khách là ký tự | 5 | "xyz" | EC1, EC10 | Báo lỗi: "Vui lòng nhập số nguyên" |

---

### b. Kiểm thử Giá trị biên (3 điểm)

#### Bước 1: Xác định các điểm biên

- **Biến Số đêm (D):** Miền [1, 30], điểm phân chia nội bộ tại 7 và 20.
  - Biên tại 1: {0, 1, 2}
  - Biên tại 7/8 (phân chia lớp): {6, 7, 8}
  - Biên tại 20/21 (phân chia lớp): {19, 20, 21}
  - Biên tại 30: {29, 30, 31}

- **Biến Số khách (K):** Miền [1, 4].
  - Biên tại 1: {0, 1, 2}
  - Biên tại 4: {3, 4, 5}

#### Bước 2: Bảng ca kiểm thử Giá trị biên

| TC ID | Mô tả | D | K | Kết quả mong đợi |
|:--:|:--|:--:|:--:|:--|
| **BVA01** | Dưới biên tối thiểu số đêm | 0 | 2 | Lỗi: Số đêm không hợp lệ |
| **BVA02** | Biên tối thiểu số đêm | 1 | 2 | Thành công. 1 × 500.000 = 500.000 VNĐ |
| **BVA03** | Ngay trên biên tối thiểu số đêm | 2 | 2 | Thành công. 2 × 500.000 = 1.000.000 VNĐ |
| **BVA04** | Ngay dưới biên phân chia 7/8 | 6 | 2 | Thành công. 6 × 500.000 = 3.000.000 VNĐ |
| **BVA05** | Tại biên 7 đêm | 7 | 2 | Thành công. 7 × 500.000 = 3.500.000 VNĐ |
| **BVA06** | Ngay trên biên 7 (chuyển sang lớp 8–20) | 8 | 2 | Thành công. 8 × 450.000 = 3.600.000 VNĐ |
| **BVA07** | Ngay dưới biên phân chia 20/21 | 19 | 2 | Thành công. 19 × 450.000 = 8.550.000 VNĐ |
| **BVA08** | Tại biên 20 đêm | 20 | 2 | Thành công. 20 × 450.000 = 9.000.000 VNĐ |
| **BVA09** | Ngay trên biên 20 (chuyển sang lớp 21–30) | 21 | 2 | Thành công. 21 × 400.000 = 8.400.000 VNĐ |
| **BVA10** | Ngay dưới biên tối đa số đêm | 29 | 2 | Thành công. 29 × 400.000 = 11.600.000 VNĐ |
| **BVA11** | Biên tối đa số đêm | 30 | 2 | Thành công. 30 × 400.000 = 12.000.000 VNĐ |
| **BVA12** | Vượt biên tối đa số đêm | 31 | 2 | Lỗi: Số đêm tối đa là 30 |
| **BVA13** | Dưới biên tối thiểu số khách | 5 | 0 | Lỗi: Số khách không hợp lệ |
| **BVA14** | Biên tối thiểu số khách | 5 | 1 | Thành công. 5 × 500.000 = 2.500.000 VNĐ |
| **BVA15** | Ngay trên biên tối thiểu số khách | 5 | 2 | Thành công. 5 × 500.000 = 2.500.000 VNĐ |
| **BVA16** | Ngay dưới biên tối đa số khách | 5 | 3 | Thành công. 5 × 500.000 = 2.500.000 VNĐ |
| **BVA17** | Biên tối đa số khách | 5 | 4 | Thành công. 5 × 500.000 = 2.500.000 VNĐ |
| **BVA18** | Vượt biên tối đa số khách | 5 | 5 | Lỗi: Số khách tối đa là 4 |

---

## CÂU 2 – LỜI GIẢI (4 điểm)

### Bước 1: Đánh số câu lệnh và xác định các nút CFG

```
Nút 1: low = 0; high = n - 1;
Nút 2: [WHILE] low <= high ?          ← điều kiện vòng lặp
Nút 3: mid = (low + high) / 2;
Nút 4: [IF] X < V[mid] ?              ← nhánh trong vòng lặp
Nút 5: high = mid - 1;
Nút 6: [ELSE IF] X > V[mid] ?
Nút 7: low = mid + 1;
Nút 8: return mid;                    ← tìm thấy
Nút 9: return -1;                     ← không tìm thấy (kết thúc)
```

### Đồ thị luồng điều khiển (CFG) – dạng văn bản

```
      [1] Khởi tạo
          |
          v
      [2] low <= high?
      /           \
  True            False
    |               |
    v               v
  [3] tính mid    [9] return -1
    |
    v
  [4] X < V[mid]?
  /         \
True        False
  |           |
  v           v
[5] high    [6] X > V[mid]?
= mid-1    /          \
  |     True          False
  |       |             |
  |     [7] low       [8] return mid
  |    = mid+1
  |       |
  +-------+
  (quay lại nút 2)
```

### Bước 2: Tính độ phức tạp Cyclomatic V(G)

- **Số nút (N):** 9
- **Số cung (E):** 12
  - 1→2, 2→3 (True), 2→9 (False), 3→4, 4→5 (True), 4→6 (False), 5→2, 6→7 (True), 6→8 (False), 7→2, 8→9, 9 (kết thúc)
- **Số nút vị từ (P):** 3 (Nút 2, Nút 4, Nút 6)

> **Công thức 1:** V(G) = E − N + 2 = 12 − 9 + 2 = **5**
>
> **Công thức 2:** V(G) = P + 1 = 3 + 1 = **4**

> **Lưu ý:** Hàm BinSearch có vòng lặp while với 3 nút điều kiện → V(G) = 4. Cần 4 đường thi hành cơ sở.

### Bước 3: Liệt kê các đường thi hành cơ sở (Basis Paths)

| STT | Đường thi hành | Mô tả |
|:--:|:--|:--|
| **P1** | 1 → 2(False) → 9 | Mảng rỗng, không vào vòng lặp |
| **P2** | 1 → 2(True) → 3 → 4(True) → 5 → 2(False) → 9 | Tìm trái, không tìm thấy |
| **P3** | 1 → 2(True) → 3 → 4(False) → 6(True) → 7 → 2(False) → 9 | Tìm phải, không tìm thấy |
| **P4** | 1 → 2(True) → 3 → 4(False) → 6(False) → 8 | Tìm thấy ngay (X == V[mid]) |

### Bước 4: Bảng ca kiểm thử

Giả sử mảng V = {2, 5, 8, 12, 16}, n = 5.

| TC ID | Input (X, V, n) | Đường đi | Số lần lặp | Kết quả mong đợi |
|:--:|:--|:--|:--:|:--|
| **TC_P1** | X=5, V=[], n=0 | 1→2(F)→9 | 0 | return -1 (mảng rỗng) |
| **TC_P2** | X=1, V={2,5,8,12,16}, n=5 | 1→2(T)→3→4(T)→5→2(F)→9 | ≥1, tìm trái, hết mảng | return -1 (không tìm thấy) |
| **TC_P3** | X=20, V={2,5,8,12,16}, n=5 | 1→2(T)→3→4(F)→6(T)→7→2(F)→9 | ≥1, tìm phải, hết mảng | return -1 (không tìm thấy) |
| **TC_P4** | X=8, V={2,5,8,12,16}, n=5 | 1→2(T)→3→4(F)→6(F)→8 | 1 | return 2 (chỉ số của 8) |

---

> **Tổng kết điểm:**
> - Câu 1a (Lớp tương đương): 3 điểm – Phân chia đủ lớp, bảng TC đủ cột, mỗi lớp ≥ 1 TC.
> - Câu 1b (Giá trị biên): 3 điểm – Xác định đúng biên, đủ BVA, ghi kết quả chính xác.
> - Câu 2 (Hộp trắng): 4 điểm – CFG đúng (1đ), V(G) đúng 2 CT (1đ), đủ Basis Paths (1đ), bảng TC đúng (1đ).
