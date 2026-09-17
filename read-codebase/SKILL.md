---
name: read-codebase
description: Trước khi thiết kế bất cứ thứ gì đụng vào code đã có.
---

# read-codebase

## Lệnh, theo thứ tự
```sh
fd -e h include/ src/ | head -40
rg "^[a-z_]+ +\*?[a-z_]+\(" include/ --no-heading | head -60
rg -n "typedef struct" include/
wc -l src/*.c | sort -n | tail -15
```

## Cách đọc
- Header trước, `.c` sau. Header là hợp đồng, `.c` là chi tiết.
- File dài nhất thường là chỗ kiến trúc đã mục. Ghi nhận, đừng sửa.
- Tìm hàm gần giống trước khi đề xuất hàm mới. Mở rộng > thêm mới.

## Báo cáo trước khi thiết kế
Luôn nói ba dòng: cái gì đã tồn tại, cái gì thiếu, cái gì sẽ phải sửa.
```