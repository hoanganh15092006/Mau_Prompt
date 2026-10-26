# 🛡️ Mau_Prompt: AI Coding Guardrails & Prompt Templates

> **Bộ khung quy chuẩn và mẫu prompt tinh gọn, tối ưu dành cho Lập trình viên khi làm việc với AI Coding Assistants (Cursor, Windsurf, GitHub Copilot, Antigravity, Claude Code, ChatGPT).**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![AI-Assisted-Coding](https://img.shields.io/badge/AI-Assisted%20Coding-8A2BE2.svg)](#)
[![Code-Quality](https://img.shields.io/badge/Quality-Production%20Ready-success.svg)](#)
[![Guardrails](https://img.shields.io/badge/Guardrails-3--Layer%20Protection-orange.svg)](#)

---

## 📌 1. Giới thiệu

Khi lập trình cùng các AI Assistant, các lập trình viên thường xuyên gặp phải những vấn đề nan giải:
* ⚠️ **Code sinh comment thừa, vô nghĩa**: AI thường giải thích những điều hiển nhiên (`// lặp qua mảng`, `// kiểm tra if`), làm loãng mã nguồn.
* ⚠️ **Thiếu an toàn kiểu dữ liệu (Type Safety)**: Lạm dụng `any`, ép kiểu vô tội vạ, nuốt lỗi (catch rỗng).
* ⚠️ **Code lạc đề, phá vỡ cấu trúc dự án**: AI tự tiện tạo file ở thư mục tùy ý, duplicate logic có sẵn.
* ⚠️ **Bỏ sót trường hợp biên (Edge Cases)**: Chỉ viết code cho "Happy Path", bỏ qua validation và xử lý lỗi thực tế.

**`Mau_Prompt`** cung cấp một giải pháp toàn diện theo phương pháp **3 Lớp Bảo Vệ (3-Layer Guardrail System)** dựa trên **Nguyên lý Đệ nhất (First Principles)**, giúp bạn kiểm soát hoàn toàn chất lượng code sinh ra từ AI.

---

## 🏗️ 2. Mô hình 3 Lớp Bảo Vệ (3-Layer Guardrails)

```
       ┌────────────────────────────────────────────────────────┐
Lớp 1  │ 📜 RULES.md: Định hình tư duy & Quy chuẩn hành vi AI   │
       │    - Không comment rác   - Strict Type Safety          │
       │    - Fail Fast           - Trả lời thẳng vào kỹ thuật  │
       └───────────────────────────┬────────────────────────────┘
                                   │
                                   ▼
       ┌────────────────────────────────────────────────────────┐
Lớp 2  │ 🗺️ ARCHITECTURE.md & SPEC.md: Bản đồ & Ranh giới code  │
       │    - Cấu trúc thư mục & trách nhiệm từng tầng          │
       │    - I/O Contract, Edge Cases & Acceptance Criteria    │
       └───────────────────────────┬────────────────────────────┘
                                   │
                                   ▼
       ┌────────────────────────────────────────────────────────┐
Lớp 3  │ 🤖 GitHub Actions CI: Cổng chặn kiểm soát tự động      │
       │    - Type Checking (tsc / mypy)                        │
       │    - Linting (eslint / flake8)                         │
       │    - Automated Tests (jest / vitest / pytest)          │
       └────────────────────────────────────────────────────────┘
```

---

## 📁 3. Cấu trúc và Chi tiết các Tài nguyên

| File | Vai trò | Mục đích & Trọng tâm |
| :--- | :--- | :--- |
| **[`RULES.md`](file:///d:/Mau_Prompt/RULES.md)** | **Quy tắc cốt lõi** | Thiết lập vai trò Principal Software Engineer cho AI. Cấm tuyệt đối comment rác, bắt buộc code tự tường minh (self-documenting), an toàn kiểu dữ liệu, phản hồi ngắn gọn không xã giao. |
| **[`ARCHITECHTURE.md`](file:///d:/Mau_Prompt/ARCHITECHTURE.md)** | **Bản đồ kiến trúc** | Nguồn sự thật duy nhất (Single Source of Truth) về cấu trúc dự án, phân tầng (`api/`, `core/`, `data/`, `shared/`, `config/`), luồng dữ liệu và quy ước đặt tên file/hàm. |
| **[`SPEC.md`](file:///d:/Mau_Prompt/SPEC.md)** | **Đặc tả tính năng** | Khung mẫu giao kèo I/O (Input/Output Contract), danh sách các trường hợp biên (Edge cases) bắt buộc xử lý và checklist nghiệm thu (Acceptance Criteria). |
| **[`cachvietarvhitechture.md`](file:///d:/Mau_Prompt/cachvietarvhitechture.md)** | **Hướng dẫn & Mẫu** | Hướng dẫn chi tiết cách tùy biến và xây dựng file `ARCHITECTURE.md` cho các dự án thực tế. |
| **[`mauchoSPEC.md`](file:///d:/Mau_Prompt/mauchoSPEC.md)** | **Hướng dẫn & Mẫu** | Bản đặc tả chi tiết mẫu cho một tính năng (ví dụ: Auth Register) cùng cách phối hợp với AI trong thực tế. |
| **[`cachvietci.md`](file:///d:/Mau_Prompt/cachvietci.md)** | **Tự động hóa CI/CD** | Mẫu cấu hình GitHub Actions (`.github/workflows/ci.yml`) cho cả TypeScript/Node.js và Python để chặn code lỗi trước khi merge. |

---

## 🚀 4. Quy trình áp dụng vào Dự án (Workflow)

### Bước 1: Khởi tạo quy chuẩn cho AI trong dự án của bạn

Copy nội dung của `RULES.md` vào vị trí phù hợp với công cụ bạn sử dụng:

* **Cursor IDE**: Dán vào `.cursorrules` hoặc file rules trong `.cursor/rules/`.
* **Windsurf / Cascade**: Dán vào `.windsurfrules`.
* **GitHub Copilot**: Dán vào `.github/copilot-instructions.md`.
* **Claude Code / Antigravity / Aider**: Đặt file `RULES.md` ở root hoặc đưa vào file system prompt / memory.

### Bước 2: Thiết lập Bản đồ Kiến trúc (`ARCHITECTURE.md`)

1. Sao chép mẫu từ `ARCHITECHTURE.md` (hoặc `cachvietarvhitechture.md`) vào thư mục gốc của dự án.
2. Tùy chỉnh mục **Tech Stack** và **Cây thư mục** theo dự án thực tế.
3. Khi ra lệnh cho AI sinh module mới hoặc refactor, tag `@ARCHITECTURE.md` vào câu lệnh.

### Bước 3: Viết Đặc tả Tính năng trước khi code (`SPEC.md`)

Trước khi yêu cầu AI viết code cho bất kỳ chức năng nào:
1. Tạo một file spec (ví dụ: `specs/user-login.md`) theo form mẫu trong `SPEC.md`.
2. Định nghĩa rõ: **Input**, **Output mong muốn**, **Edge Cases** (Dữ liệu trùng, thiếu trường, timeout, khoảng trắng thừa...).
3. Checklist nghiệm thu (Acceptance Criteria).

### Bước 4: Prompting chuẩn kỹ thuật (Prompt Mẫu)

Sử dụng quy trình TDD (Test-Driven Development) khi giao việc cho AI:

```markdown
Đọc kỹ @RULES.md, @ARCHITECTURE.md và @specs/user-login.md.

Thực hiện theo các bước sau:
1. Viết bộ kiểm thử tự động (Unit Test) bao phủ toàn bộ các trường hợp thành công và các Edge Cases trong spec.
2. Viết mã nguồn triển khai tính năng để toàn bộ test trên pass 100%.
3. Đảm bảo đặt file đúng cấu trúc trong @ARCHITECTURE.md và tuân thủ nguyên tắc không comment rác trong @RULES.md.
```

### Bước 5: Kích hoạt CI bảo vệ tự động

1. Tạo thư mục `.github/workflows/` trong repo của bạn.
2. Tạo file `ci.yml` và copy cấu hình tương ứng từ `cachvietci.md` (Node.js/TypeScript hoặc Python).
3. Mỗi khi đẩy code lên GitHub, CI sẽ tự động chạy:
   - ✅ Kiểm tra kiểu dữ liệu tĩnh (`tsc --noEmit` hoặc `mypy . --strict`).
   - ✅ Linting code (`npm run lint` hoặc `flake8`).
   - ✅ Kiểm thử tự động (`npm test` hoặc `pytest`).

---

## 💡 5. Các Mẫu Prompt Thực Chiến

### 1. Fix Bug (Sửa lỗi triệt để)
```text
@RULES.md Hãy phân tích lỗi sau đây:
[Dán log lỗi hoặc mô tả hành vi sai]

Yêu cầu:
1. Nêu chính xác nguyên nhân gốc rễ (root cause) trong tối đa 2 gạch đầu dòng.
2. Trả về ngay khối code đã sửa chữa, không giải thích dài dòng.
```

### 2. Refactor Code (Tái cấu trúc chuẩn kiến trúc)
```text
Đọc @RULES.md và @ARCHITECTURE.md.
Hãy refactor lại file [đường dẫn file] để:
1. Tách nhỏ các hàm vi phạm Single Responsibility.
2. Đưa các hàm tiện ích thuần túy về đúng tầng `shared/`.
3. Loại bỏ hoàn toàn mọi comment rác, chỉ giữ lại code self-documenting và type safety nghiêm ngặt.
```

---

## 🎯 6. Nguyên tắc Vàng (Core Philosophy)

* 🚫 **Zero Comment Clutter**: Code tốt nhất là code tự giải thích chính nó thông qua tên hàm, biến và cấu trúc rõ ràng.
* ⚡ **Fail Fast & Guard Clauses**: Kiểm tra dữ liệu và return sớm, tránh lồng ghép `if-else` phức tạp.
* 🔒 **Strict Type Safety**: Loại bỏ hoàn toàn `any`. Mọi ranh giới dữ liệu đều phải được validate bằng Schema/DTO.
* 🎯 **Single Responsibility**: Mỗi hàm, mỗi file chỉ đảm nhiệm đúng một việc duy nhất.

---

## 🤝 7. Đóng góp & Giấy phép

Mọi đóng góp, câu hỏi hoặc cải tiến prompt đều được hoan nghênh! Hãy mở một Issue hoặc tạo Pull Request.

Dự án được phân phối dưới giấy phép **MIT License**.