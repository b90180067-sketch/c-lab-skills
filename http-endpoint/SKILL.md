---
name: http-endpoint
description: Khi thêm hoặc sửa endpoint HTTP.
---

# http-endpoint

## Trước khi viết
Đọc `docs/ref/rfc9112.txt` §3 (request line) và §6 (message body) cho
bất cứ thứ gì đụng parser. Không nhớ từ đầu.

## Checklist mỗi endpoint
- [ ] Giới hạn độ dài request line và mỗi header. Từ chối 431 khi vượt.
- [ ] Giới hạn body size. Từ chối 413. Con số nằm trong config, không hardcode.
- [ ] Path đi qua hàm chuẩn hoá, chặn `..` và `//`. Test cả `%2e%2e`.
- [ ] Đóng fd trên **mọi** nhánh return, kể cả nhánh lỗi.
- [ ] Không `printf` thẳng dữ liệu người dùng vào format string.
- [ ] Response luôn có Content-Length hoặc chunked. Không để trống.
- [ ] Test có ít nhất một input dị dạng, không chỉ input hợp lệ.

## Bẫy hay gặp
- `read()` trả về ít hơn yêu cầu là bình thường, không phải lỗi. Lặp.
- `read()` trả 0 là EOF, trả -1 mới là lỗi, và `EINTR` phải retry.
- Header có thể lặp lại. Quyết định trong spec, không tự chọn.
```