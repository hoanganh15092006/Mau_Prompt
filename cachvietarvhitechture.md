Dưới đây là mẫu chuẩn cho file `ARCHITECTURE.md` bằng tiếng Việt. File này đóng vai trò là "bản đồ địa hình" để AI hiểu rõ ranh giới dự án, không bao giờ tạo file bừa bãi hay duplicate logic.

Bạn có thể lưu mẫu này vào file `ARCHITECTURE.md` ở thư mục gốc của dự án và điền thông tin tương ứng:

```markdown
# KIẾN TRÚC HỆ THỐNG DỰ ÁN (PROJECT ARCHITECTURE)

Tài liệu này là nguồn sự thật duy nhất (Single Source of Truth) về cấu trúc dự án. 
Mọi tác vụ sinh code, tạo file mới hoặc refactor của AI bắt buộc phải tuân theo cấu trúc dưới đây.

---

## 1. TỔNG QUAN HỆ THỐNG
- **Tên dự án:** [Ví dụ: E-Commerce API / Task Management App]
- **Mục tiêu cốt lõi:** [Mô tả ngắn gọn hệ thống làm nhiệm vụ gì trong 1-2 câu]
- **Tech Stack chính:**
  - Runtime / Ngôn ngữ: [Ví dụ: Node.js 20 / TypeScript 5.x hoặc Python 3.12]
  - Framework: [Ví dụ: Next.js 15 (App Router) hoặc FastAPI]
  - Cơ sở dữ liệu & ORM: [Ví dụ: PostgreSQL + Prisma hoặc SQLite + SQLAlchemy]
  - Quản lý State / Thư viện phụ trợ: [Ví dụ: Zustand, Zod, Tailwind CSS]

---

## 2. CÂY THƯ MỤC VÀ TRÁCH NHIỆM TỪNG PHẦN
*AI không được tự ý tạo thêm các thư mục nằm ngoài cấu trúc đã định nghĩa dưới đây:*

```text
src/
├── api/             # Điểm tiếp nhận request, định tuyến (Routers/Controllers)
├── core/            # Logic nghiệp vụ độc lập (Business Logic, Services)
├── data/            # Giao tiếp cơ sở dữ liệu, Repository, Schema ORM
├── shared/          # Các hàm tiện ích thuần túy (pure helpers), Constants, Types
└── config/          # Biến môi trường, cấu hình client DB/Third-party

```

**Quy tắc phân tầng:**

1. `api/` chỉ làm nhiệm vụ parse request, validate input và gọi sang `core/`. Không viết logic nghiệp vụ tại đây.
2. `core/` chỉ xử lý logic tính toán, không truy vấn trực tiếp DB; phải gọi qua `data/`.
3. `shared/` chỉ chứa các hàm thuần túy (pure functions), không phụ thuộc vào trạng thái hệ thống.

---

## 3. LUỒNG DỮ LIỆU CHUẨN (DATA FLOW)

Mọi luồng dữ liệu khi thực thi một tác vụ đều phải đi qua các bước tuần tự sau:

`Client Request`
➔ **Validation Layer** (Kiểm tra Schema/Type bằng Zod hoặc Pydantic)
➔ **Service / Core Layer** (Thực thi logic nghiệp vụ)
➔ **Data Layer / Repository** (Đọc/Ghi cơ sở dữ liệu)
➔ **Response Formatter** (Đóng gói kết quả chuẩn trả về cho Client)

---

## 4. QUY ƯỚC ĐẶT TÊN & TỔ CHỨC FILE (CONVENTIONS)

* **Tên file & thư mục:** Dùng `kebab-case` (ví dụ: `user-profile.service.ts`, `auth-middleware.ts`).
* **Tên Class / Interface / Type:** Dùng `PascalCase` (ví dụ: `UserProfile`, `CreateOrderDTO`).
* **Tên biến & hàm:** Dùng `camelCase` (ví dụ: `calculateTotalPrice`, `isActiveUser`).
* **Tổ chức Module:** Gom nhóm theo tính năng (Feature-based) hoặc theo tầng (Layer-based), không đặt file lung tung ngoài thư mục chỉ định.

---

## 5. CÁC HÀM TIỆN ÍCH DÙNG CHUNG CÓ SẴN (SHARED UTILS)

*Khi cần các tính năng sau, AI phải tái sử dụng từ shared, không được tự viết lại:*

* **Logger:** Import từ `src/shared/logger`
* **Database Client:** Import instance đã khởi tạo tại `src/config/database`
* **Custom Errors:** Sử dụng các class lỗi chuẩn định nghĩa sẵn tại `src/shared/errors`

```

---

### Cách dùng:
Chỉ cần sửa lại phần **Tech Stack** và **Cây thư mục** cho đúng với dự án thực tế của bạn. Mỗi khi mở phiên làm việc mới với Cursor hoặc các AI khác, bạn tag `@ARCHITECTURE.md` vào để AI luôn nhớ vị trí cần đặt file và cách tổ chức luồng code.

```