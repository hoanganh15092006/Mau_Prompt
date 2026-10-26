# ĐẶC TẢ TÍNH NĂNG (FEATURE SPECIFICATION)

- **Tên tính năng:** [Ví dụ: Đăng ký tài khoản người dùng mới / Tính năng Giỏ hàng]
- **Mục tiêu:** [Giải thích trong 1 câu: Tính năng này giải quyết vấn đề gì cho hệ thống/người dùng]
- **Trạng thái:** [Chưa làm / Đang thực hiện / Đã hoàn thành]

---

## 1. GIAO KÈO ĐẦU VÀO VÀ ĐẦU RA (INPUT / OUTPUT CONTRACT)

### Đầu vào (Input):
- **Endpoint / Method / Function:** [Ví dụ: `POST /api/v1/auth/register` hoặc hàm `registerUser()`]
- **Tham số bắt buộc:**
  - `email`: Chuỗi (string), định dạng email chuẩn, không phân biệt hoa thường.
  - `password`: Chuỗi (string), độ dài từ 8 đến 32 ký tự, chứa ít nhất 1 chữ số và 1 ký tự đặc biệt.
  - `fullName`: Chuỗi (string), độ dài từ 2 đến 50 ký tự.
- **Tham số tùy chọn (nếu có):**
  - `phoneNumber`: Chuỗi hoặc null.

### Đầu ra (Output):
- **Trường hợp thành công (Success - HTTP 201):**
  ```json
  {
    "success": true,
    "data": {
      "userId": "usr_123456",
      "email": "user@example.com",
      "createdAt": "2026-10-26T08:00:00Z"
    }
  }