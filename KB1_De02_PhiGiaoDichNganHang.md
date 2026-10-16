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
