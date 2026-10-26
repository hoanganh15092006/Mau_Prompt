Dưới đây là mẫu file CI hoàn chỉnh cho **GitHub Actions**, đóng vai trò là "lớp bảo vệ tự động bên ngoài" để chặn mọi lỗi lặt vặt của AI trước khi code được merge.

Tạo đúng đường dẫn file trong repo của bạn:

`.github/workflows/ci.yml`

---

### Mẫu 1: Dành cho dự án JavaScript / TypeScript (Node.js, Next.js, Express, React...)

```yaml
name: Strict AI Guardrail CI

# Chạy tự động mỗi khi có commit mới đẩy lên main hoặc khi mở Pull Request
on:
  push:
    branches: [main, master, develop]
  pull_request:
    branches: [main, master, develop]

jobs:
  code-verification:
    name: Verify Code Integrity
    runs-on: ubuntu-latest

    steps:
      # 1. Kéo mã nguồn về máy ảo CI
      - name: Checkout repository
        uses: actions/checkout@v4

      # 2. Khởi tạo môi trường Node.js
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'npm' # hoặc 'pnpm' / 'yarn'

      # 3. Cài đặt dependencies chính xác theo lockfile
      - name: Install dependencies
        run: npm ci

      # 4. Kiểm tra kiểu dữ liệu nghiêm ngặt (Chặn việc AI ép kiểu ẩu)
      - name: Step 1 - Strict Type Check
        run: npx tsc --noEmit

      # 5. Soi chuẩn code (Chặn biến thừa, import rác, code bẩn)
      - name: Step 2 - Linting Check
        run: npm run lint

      # 6. Chạy toàn bộ test tự động (Kiểm tra edge cases đã viết trong SPEC.md)
      - name: Step 3 - Run Automated Tests
        run: npm test

```

---

### Mẫu 2: Dành cho dự án Python (FastAPI, Django, Flask, script...)

```yaml
name: Strict AI Guardrail CI

on:
  push:
    branches: [main, master, develop]
  pull_request:
    branches: [main, master, develop]

jobs:
  code-verification:
    name: Verify Code Integrity
    runs-on: ubuntu-latest

    steps:
      # 1. Kéo mã nguồn về
      - name: Checkout repository
        uses: actions/checkout@v4

      # 2. Cài đặt môi trường Python
      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.12'
          cache: 'pip'

      # 3. Cài dependencies
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
          pip install mypy flake8 pytest pytest-cov

      # 4. Kiểm tra Type Hints nghiêm ngặt bằng mypy
      - name: Step 1 - Strict Type Check
        run: mypy . --strict

      # 5. Kiểm tra cú pháp và code rác bằng flake8
      - name: Step 2 - Linting Check
        run: flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics

      # 6. Chạy bộ test tự động bằng pytest
      - name: Step 3 - Run Tests
        run: pytest

```

---

### Cách kiểm tra hoạt động:

1. Tạo thư mục `.github/workflows/` ngay tại root dự án.
2. Thả file `ci.yml` vào đó.
3. Commit và push lên GitHub (`git add .`, `git commit -m "add ci"`, `git push`).
4. Mở repo trên GitHub, bấm vào tab **Actions**: Bạn sẽ thấy tiến trình chạy tự động hiển thị tích xanh (Pass) hoặc dấu chéo đỏ (Failed).