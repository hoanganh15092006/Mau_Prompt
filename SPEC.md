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
  ```

- **Trường hợp lỗi (Error - HTTP 4xx / 5xx):**
  ```json
  {
    "success": false,
    "error": {
      "code": "EMAIL_ALREADY_EXISTS",
      "message": "Email này đã được sử dụng."
    }
  }
  ```

---

## 2. CÁC TRƯỜNG HỢP BIÊN BẮT BUỘC XỬ LÝ (EDGE CASES)

*AI phải viết code và test case bao phủ toàn bộ các tình huống sau:*

1. **Dữ liệu trùng lặp:** Email đã tồn tại trong database ➔ Trả về mã lỗi xung đột `409 Conflict`, không được để crash query.
2. **Dữ liệu thiếu / sai định dạng:** Input thiếu trường hoặc email sai cú pháp ➔ Bị chặn ngay từ tầng validate schema, trả về `400 Bad Request`.
3. **Mất kết nối Cơ sở dữ liệu / Timeout:** Không để treo request ➔ Trả về lỗi `503 Service Unavailable` và log lỗi nội bộ.
4. **Khoảng trắng thừa:** Input có khoảng trắng ở đầu hoặc cuối (` user@example.com `) ➔ Tự động `trim()` làm sạch trước khi lưu.

---

## 3. CHECKLIST NGHIỆM THU (ACCEPTANCE CRITERIA)

*Tính năng chỉ được xem là hoàn thành khi đáp ứng đủ các tiêu chí dưới đây:*

- [ ] Schema validation được áp dụng chặt chẽ trước khi dữ liệu đi vào tầng xử lý logic.
- [ ] Mật khẩu phải được hash an toàn (dùng bcrypt/argon2) trước khi lưu vào database, tuyệt đối không lưu plain text.
- [ ] Tuân thủ tuyệt đối `RULES.md`: Không viết comment rác, type safety nghiêm ngặt.
- [ ] Đặt file đúng vị trí quy định trong `ARCHITECTURE.md`.
- [ ] Toàn bộ Unit Test kiểm tra các case thành công và 4 Edge Cases ở Mục 2 đều pass 100%.