---
name: build-verify
description: Chạy trước mọi lần báo hoàn thành, hoặc khi build đỏ.
---

# build-verify

## Lệnh, đúng thứ tự
```sh
make clean && make 2>&1 | tee /tmp/build.log
grep -nE "error|warning" /tmp/build.log | head -20
make test 2>&1 | tail -30
echo "exit=$?"
```

## Đọc lỗi
- Sửa **lỗi đầu tiên**, build lại. Lỗi 2..n thường là hệ quả.
- `implicit declaration of function` → thiếu include, không phải thiếu hàm.
- `dereferencing pointer to incomplete type` → struct mới forward-declare,
  cần include header định nghĩa nó. Không phải cast.
- `-Wunused-parameter` → `(void)param;` một dòng đầu hàm. Không đổi chữ ký để né.
- `-Wsign-compare` → sửa kiểu cho đúng. Không cast để tắt cảnh báo.
- ASan `heap-use-after-free` → đọc cả hai stack trace: chỗ free và chỗ dùng.

## Không được làm
- Thêm `-Wno-*` vào Makefile.
- Comment out test để build xanh.
- Báo xong khi `make test` chưa exit 0.