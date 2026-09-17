---
name: sanitize
description: Pass kiểm tra chuẩn trên toàn bộ codebase.
---

# sanitize

## Ba lần build, ba loại lỗi khác nhau
```sh
# 1. ASan + UBSan — bộ nhớ và undefined behavior
make clean && make CFLAGS="-std=c11 -g -O1 -fsanitize=address,undefined \
  -fno-omit-frame-pointer -Wall -Wextra" 2>&1 | tail -20
ASAN_OPTIONS=detect_leaks=1:abort_on_error=0 make test 2>&1 | tee /tmp/asan.log

# 2. MSan — đọc bộ nhớ chưa khởi tạo (clang only)
make clean && make CC=clang CFLAGS="-std=c11 -g -O1 -fsanitize=memory \
  -fno-omit-frame-pointer" && make test 2>&1 | tee /tmp/msan.log

# 3. valgrind — bắt được thứ ASan bỏ sót ở biên syscall
make clean && make CFLAGS="-std=c11 -g -O0"
valgrind --leak-check=full --track-origins=yes ./tests/test_all 2>&1 | tee /tmp/vg.log
```

## Đọc kết quả
- `SUMMARY: AddressSanitizer: heap-buffer-overflow` → đọc dòng
  `allocated by thread` để biết buffer thật dài bao nhiêu.
- `runtime error: signed integer overflow` (UBSan) → thường là hygiene,
  trừ khi giá trị đó thành độ dài buffer. Kiểm tra dòng dùng nó.
- valgrind `Conditional jump depends on uninitialised value` → truy
  `--track-origins` để ra chỗ cấp phát.
- ASan + valgrind cùng lúc là vô nghĩa. Chạy riêng.

## Không được làm
- Đặt `ASAN_OPTIONS=detect_leaks=0` để báo cáo sạch hơn.
- Bỏ qua UBSan vì "chỉ là cảnh báo".
```