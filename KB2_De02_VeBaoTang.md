# ĐỀ THI GIỮA KỲ – MÔN KIỂM THỬ PHẦN MỀM
## **ĐỀ 02 – KỊCH BẢN 2**
### Thời gian: 60 phút | Được sử dụng tài liệu: Không

---

## CÂU 1 (6 ĐIỂM) – KIỂM THỬ HỘP ĐEN (Black-box Testing)

### Đặc tả bài toán: Hệ thống tính tiền vé và phát mũ tham quan bảo tàng

Bảo tàng quốc gia áp dụng chính sách bán vé và tặng quà lưu niệm như sau:

**Chính sách vé:**

| Độ tuổi khách tham quan | Giá vé |
|:--|:--|
| Dưới 5 tuổi | Miễn phí (0 VNĐ) |
| Từ 5 đến 65 tuổi | 40.000 VNĐ/vé |
| Trên 65 tuổi | 20.000 VNĐ/vé |

**Chính sách tặng mũ lưu niệm:**

| Giới tính | Màu mũ tặng |
|:--|:--|
| Khách Nữ | Mũ màu Hồng |
| Khách Nam | Mũ màu Xanh |

---

### Áp dụng kỹ thuật Kiểm thử Bảng quyết định (Decision Table Testing) (6 điểm)

**Yêu cầu:**
1. Xác định các điều kiện (Conditions) và hành động (Actions) của bài toán.
2. Xây dựng **Bảng quyết định (Decision Table)** đầy đủ với tất cả các tổ hợp điều kiện.
3. Thiết kế **ca kiểm thử (Test Cases)** tương ứng cho mỗi quy tắc trong bảng quyết định. Ghi rõ: Mã TC, dữ liệu đầu vào (tuổi, giới tính), kết quả mong đợi (giá vé, màu mũ).

---

## CÂU 2 (4 ĐIỂM) – KIỂM THỬ HỘP TRẮNG (White-box Testing)

### Mã nguồn:

```c
int calculate_fee(int amount)
{
    int fee = 0;
    if (amount > 0)
    {
        if (amount <= 100000)
            fee = 5000;
        else if (amount <= 500000)
            fee = 10000;
        else
            fee = amount * 0.02;
    }
    return fee;
}
```

> **Chú thích:** `amount`: Số tiền giao dịch (VNĐ). Trả về `fee` – phí dịch vụ cần trả.

**Yêu cầu:**
1. Vẽ Đồ thị luồng điều khiển (CFG) của hàm trên. Đánh số nút rõ ràng.
2. Tính độ phức tạp Cyclomatic V(G) bằng hai công thức khác nhau.
3. Xác định tập các đường thi hành cơ sở (Basis Paths) và liệt kê đầy đủ V(G) đường độc lập.
4. Áp dụng tiêu chí **Kiểm thử đường cơ bản (Basis Path Testing – McCabe)**: Thiết kế bảng ca kiểm thử tương ứng cho từng đường (ghi rõ Input, đường đi, kết quả mong đợi).

---

### Hết

---
---

# LỜI GIẢI CHI TIẾT – ĐỀ 02 KỊCH BẢN 2

---

## CÂU 1 – LỜI GIẢI (6 điểm)

### Bước 1: Xác định Điều kiện và Hành động

**Các điều kiện (Conditions):**

| Ký hiệu | Điều kiện | Giá trị có thể |
|:--:|:--|:--|
| **C1** | Độ tuổi khách | < 5 tuổi / 5–65 tuổi / > 65 tuổi (3 giá trị) |
| **C2** | Giới tính | Nam / Nữ (2 giá trị) |

**Các hành động (Actions):**

| Ký hiệu | Hành động |
|:--:|:--|
| **A1** | Vé miễn phí (0 VNĐ) |
| **A2** | Vé 40.000 VNĐ |
| **A3** | Vé 20.000 VNĐ |
| **A4** | Tặng mũ Hồng |
| **A5** | Tặng mũ Xanh |

---

### Bước 2: Bảng quyết định (Decision Table)

C1 có 3 giá trị × C2 có 2 giá trị = **6 tổ hợp (Rules)**:

| Điều kiện / Hành động | R1 | R2 | R3 | R4 | R5 | R6 |
|:--|:--:|:--:|:--:|:--:|:--:|:--:|
| **C1: Độ tuổi** | < 5 | < 5 | 5–65 | 5–65 | > 65 | > 65 |
| **C2: Giới tính** | Nữ | Nam | Nữ | Nam | Nữ | Nam |
| **A1: Vé 0đ** | **X** | **X** | | | | |
| **A2: Vé 40.000đ** | | | **X** | **X** | | |
| **A3: Vé 20.000đ** | | | | | **X** | **X** |
| **A4: Mũ Hồng** | **X** | | **X** | | **X** | |
| **A5: Mũ Xanh** | | **X** | | **X** | | **X** |

---

### Bước 3: Bảng ca kiểm thử

| TC ID | Tuổi | Giới tính | Rule | Giá vé | Màu mũ |
|:--:|:--:|:--:|:--:|:--:|:--:|
| **TC01** | 3 | Nữ | R1 | 0 VNĐ (Miễn phí) | Mũ Hồng |
| **TC02** | 4 | Nam | R2 | 0 VNĐ (Miễn phí) | Mũ Xanh |
| **TC03** | 30 | Nữ | R3 | 40.000 VNĐ | Mũ Hồng |
| **TC04** | 25 | Nam | R4 | 40.000 VNĐ | Mũ Xanh |
| **TC05** | 70 | Nữ | R5 | 20.000 VNĐ | Mũ Hồng |
| **TC06** | 75 | Nam | R6 | 20.000 VNĐ | Mũ Xanh |

---

## CÂU 2 – LỜI GIẢI (4 điểm)

### Bước 1: Đánh số câu lệnh và xác định các nút CFG

```
Nút 1: fee = 0;
Nút 2: [IF] amount > 0 ?
Nút 3: [IF] amount <= 100000 ?
Nút 4: fee = 5000;
Nút 5: [ELSE IF] amount <= 500000 ?
Nút 6: fee = 10000;
Nút 7: fee = amount * 0.02;
Nút 8: return fee;
```

### Sơ đồ CFG (dạng văn bản)

```
[1] fee = 0
     |
     v
[2] amount > 0 ?
   /          \
True          False
  |             |
  v             |
[3] amount <= 100000 ?   |
  /         \            |
True        False        |
  |           |          |
  v           v          |
[4] fee=5000 [5] amount <= 500000 ?
  |           /         \
  |        True         False
  |          |            |
  |         [6] fee=10000 [7] fee=amount*0.02
  |          |            |
  +----------+-----------+
              |
              v
           [8] return fee
```

### Bước 2: Tính độ phức tạp Cyclomatic V(G)

- **Số nút (N):** 8
- **Số cung (E):** 10
  - 1→2, 2→3(True), 2→8(False), 3→4(True), 3→5(False), 4→8, 5→6(True), 5→7(False), 6→8, 7→8
- **Số nút vị từ (P):** 3 (Nút 2, Nút 3, Nút 5)

> **Công thức 1:** V(G) = E − N + 2 = 10 − 8 + 2 = **4**
>
> **Công thức 2:** V(G) = P + 1 = 3 + 1 = **4**

→ Cần **4 đường thi hành cơ sở (Basis Paths)**.

### Bước 3: Liệt kê 4 đường thi hành cơ sở

| STT | Đường thi hành | Mô tả |
|:--:|:--|:--|
| **P1** | 1 → 2(False) → 8 | amount ≤ 0, không tính phí |
| **P2** | 1 → 2(True) → 3(True) → 4 → 8 | 0 < amount ≤ 100.000 → phí 5.000 |
| **P3** | 1 → 2(True) → 3(False) → 5(True) → 6 → 8 | 100.000 < amount ≤ 500.000 → phí 10.000 |
| **P4** | 1 → 2(True) → 3(False) → 5(False) → 7 → 8 | amount > 500.000 → phí 2% |

### Bước 4: Bảng ca kiểm thử (Basis Path Testing)

| TC ID | Input (amount) | Đường đi | fee (Kết quả mong đợi) |
|:--:|--:|:--|--:|
| **TC_P1** | -1000 | 1→2(F)→8 | 0 (amount ≤ 0, không tính phí) |
| **TC_P2** | 50.000 | 1→2(T)→3(T)→4→8 | 5.000 VNĐ |
| **TC_P3** | 300.000 | 1→2(T)→3(F)→5(T)→6→8 | 10.000 VNĐ |
| **TC_P4** | 1.000.000 | 1→2(T)→3(F)→5(F)→7→8 | 20.000 VNĐ (= 1.000.000 × 2%) |

---

> **Tổng kết điểm:**
> - Câu 1 (Bảng quyết định): 6 điểm – Xác định C và A đúng (1đ), bảng 6 rules đủ (2đ), bảng TC đúng (3đ).
> - Câu 2 (Hộp trắng – Basis Path): 4 điểm – CFG đúng (1đ), V(G)=4 bằng 2 công thức (1đ), đủ 4 Basis Paths (1đ), bảng TC đúng (1đ).
