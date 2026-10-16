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
