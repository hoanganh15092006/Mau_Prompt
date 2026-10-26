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