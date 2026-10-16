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

> **Chú thích:** Hàm kiểm tra đăng nhập.
> Trả về: 0 = Thất bại, 1 = Đăng nhập thành công (user thường), 2 = Đăng nhập thành công (admin).

**Yêu cầu:**
1. Vẽ Đồ thị luồng điều khiển (CFG) của hàm trên. Đánh số nút rõ ràng.
2. Tính độ phức tạp Cyclomatic V(G) bằng hai công thức khác nhau.
3. Liệt kê tất cả các **câu lệnh** và **quyết định (nhánh)** trong hàm.
4. Thiết kế bảng ca kiểm thử thỏa mãn đồng thời hai tiêu chí:
   - **Bao phủ câu lệnh (Statement Coverage):** Mọi câu lệnh phải được thực thi ít nhất một lần.
   - **Bao phủ quyết định (Decision Coverage):** Mọi nhánh True/False của mỗi điều kiện phải được thực thi.
   
   Ghi rõ: Mã TC, dữ liệu đầu vào, các câu lệnh/nhánh được bao phủ, kết quả mong đợi.

---

### Hết
