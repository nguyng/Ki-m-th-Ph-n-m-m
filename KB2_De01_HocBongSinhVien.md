# ĐỀ THI GIỮA KỲ – MÔN KIỂM THỬ PHẦN MỀM
## **ĐỀ 01 – KỊCH BẢN 2**
### Thời gian: 60 phút | Được sử dụng tài liệu: Không

---

## CÂU 1 (6 ĐIỂM) – KIỂM THỬ HỘP ĐEN (Black-box Testing)

### Đặc tả bài toán: Hệ thống xét học bổng sinh viên

Một trường đại học xét học bổng cho sinh viên dựa trên **ba điều kiện** sau:

- **C1 – Điểm trung bình tích lũy (GPA):** Đạt từ **3.2 trở lên** (thang 4.0) là điều kiện học lực tốt.
- **C2 – Số tín chỉ đã hoàn thành:** Đã tích lũy từ **60 tín chỉ trở lên**.
- **C3 – Tình trạng kỷ luật:** Không có cảnh cáo kỷ luật trong học kỳ hiện tại.

**Các mức học bổng:**

| Điều kiện thỏa mãn | Mức học bổng |
|:--|:--|
| Cả 3 điều kiện đều đạt | Học bổng Xuất sắc – 100% học phí |
| Chỉ C1 và C3 đạt (thiếu C2) | Học bổng Khuyến khích – 50% học phí |
| Chỉ C1 đạt (thiếu C2 hoặc C3) | Học bổng Tiềm năng – 20% học phí |
| Không đạt C1 | Không được học bổng |

---

### Áp dụng kỹ thuật Kiểm thử Bảng quyết định (Decision Table Testing) (6 điểm)

**Yêu cầu:**
1. Xác định các điều kiện (Conditions) và hành động (Actions) của bài toán.
2. Xây dựng **Bảng quyết định (Decision Table)** đầy đủ với tất cả các tổ hợp điều kiện có thể.
3. Thiết kế **ca kiểm thử (Test Cases)** tương ứng cho mỗi quy tắc (rule) trong bảng quyết định. Ghi rõ: Mã TC, dữ liệu đầu vào, kết quả mong đợi.

---

## CÂU 2 (4 ĐIỂM) – KIỂM THỬ HỘP TRẮNG (White-box Testing)

### Mã nguồn:

```c
int classify(int score, int attendance, int passed)
{
    int result = 0;
    if (score >= 5 || (attendance >= 80 && passed == 1))
    {
        if (score >= 8)
            result = 3;
        else if (score >= 6)
            result = 2;
        else
            result = 1;
    }
    return result;
}
```

> **Chú thích:** Hàm phân loại kết quả học tập.
> `score`: Điểm số (0–10), `attendance`: % chuyên cần (0–100), `passed`: Đã nộp đủ bài tập (1: có, 0: không).
> Trả về: 3 = Giỏi, 2 = Khá, 1 = Trung bình, 0 = Không đạt.

**Yêu cầu:**
1. Vẽ Đồ thị luồng điều khiển (CFG) của hàm trên. Đánh số nút rõ ràng.
2. Tính độ phức tạp Cyclomatic V(G) bằng hai công thức khác nhau.
3. Liệt kê tất cả các **đường thi hành (paths)** thỏa mãn tiêu chí **Bao phủ nhánh và điều kiện (Branch & Condition Coverage)**.
4. Thiết kế bảng ca kiểm thử tương ứng (ghi rõ Input, nhánh/điều kiện được bao phủ, kết quả mong đợi).

---

### Hết
