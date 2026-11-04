# BÀI 2: SỰ CỐ PHIÊN LÀM VIỆC TRÊN HỆ THỐNG VẬN TẢI

**Lớp:** K26CNTT2
**Môn học:** Nhập Môn Công Nghệ Thông Tin (IT108)  
**Mã sinh viên:** N26DTCN030  
**Họ và tên:** Lê Hồ Thanh Thảo  

---

## 📌 PHẦN 1: PHÂN TÍCH

**So sánh sự đánh đổi giữa dung lượng Cache và Cookies trong lưu trữ dữ liệu người dùng:**

| Tiêu chí | Cache (Bộ nhớ đệm) | Cookies |
| :--- | :--- | :--- |
| **Dung lượng** | Rất lớn (Có thể lên tới vài chục MB đến vài GB). | Rất nhỏ (Tối đa khoảng ~4KB mỗi cookie). |
| **Mục đích chính** | Lưu trữ tài nguyên tĩnh (hình ảnh, CSS, JS, HTML) giúp tăng tốc độ tải trang ở những lần truy cập sau. | Lưu trữ trạng thái phiên làm việc (session), định danh người dùng và các tùy chọn cá nhân hóa. |
| **Đánh đổi & Ứng dụng** | Tốn dung lượng ổ cứng nhưng giảm tải băng thông mạng. **Không phù hợp** để lưu token đăng nhập do không có cơ chế bảo mật truyền tải tự động theo request. | Bị giới hạn dung lượng nghiêm ngặt và luôn đính kèm vào mỗi HTTP Request (làm tăng nhẹ dung lượng gói tin). **Cực kỳ phù hợp** để lưu trữ Token định danh vì trình duyệt tự động quản lý. |

**Kết luận:** Để duy trì trạng thái giỏ hàng và phiên đăng nhập cho shipper, **Cookies** là lựa chọn tối ưu và duy nhất phù hợp.

---

## ⚙️ PHẦN 2: TRIỂN KHAI

Để giải quyết vấn đề phiên làm việc bị mất khi tải lại trang và đảm bảo tính bảo mật, cấu trúc mẩu tin Cookie (Persistent Cookie) cần được thiết lập như sau:

```http
Set-Cookie: session_token=[Mã_Token_Định_Danh]; Max-Age=604800; HttpOnly; Secure; SameSite=Strict
```
