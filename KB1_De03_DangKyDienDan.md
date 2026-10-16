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
