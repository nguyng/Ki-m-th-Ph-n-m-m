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

> **Chú thích:** Hàm tính phí dịch vụ.
> `amount`: Số tiền giao dịch (VNĐ).
> Trả về: `fee` – phí dịch vụ cần trả.

**Yêu cầu:**
1. Vẽ Đồ thị luồng điều khiển (CFG) của hàm trên. Đánh số nút rõ ràng.
2. Tính độ phức tạp Cyclomatic V(G) bằng hai công thức khác nhau.
3. Xác định tập các đường thi hành cơ sở (Basis Paths) và liệt kê đầy đủ V(G) đường độc lập.
4. Áp dụng tiêu chí **Kiểm thử đường cơ bản (Basis Path Testing – McCabe)**: Thiết kế bảng ca kiểm thử tương ứng cho từng đường (ghi rõ Input, đường đi, kết quả mong đợi).

---

### Hết
