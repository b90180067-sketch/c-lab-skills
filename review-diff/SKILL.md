---
name: review-diff
description: Khi được đưa một PR hoặc một diff để soi.
---

# review-diff

## Lệnh
```sh
git diff main...HEAD --stat
git diff main...HEAD -- '*.c' '*.h'
```

## Checklist, theo thứ tự ưu tiên
1. **Bộ nhớ** — mọi malloc mới có free trên **mọi** nhánh return?
   Đọc kỹ nhánh lỗi, đó là chỗ leak sống.
2. **Độ dài** — mọi buffer nhận input ngoài có tham số độ dài? Có chỗ
   nào dùng độ dài từ header thay vì từ số byte thật đọc được không?
3. **Số nguyên** — có phép `len - 1` nào mà `len` có thể bằng 0 không?
   Có `int` nào giữ size_t không?
4. **Tài nguyên** — fd, FILE*, mutex có đóng/mở khoá trên mọi nhánh?
5. **Hàm cấm** — `rg -n "strcpy|strcat|sprintf|gets|atoi|alloca"`.
6. **Makefile** — file mới có trong OBJS? Có `-Wno-*` nào mới lẻn vào?
7. **Test** — có test cho nhánh lỗi, không chỉ nhánh thành công?

## Cách viết nhận xét
Mỗi nhận xét gắn `file.c:LINE`. Không có dòng cụ thể thì không phải
nhận xét, chỉ là cảm giác.
```