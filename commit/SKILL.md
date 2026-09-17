---
name: commit
description: Sau khi build xanh và test exit 0.
---

# commit

## Điều kiện
Không commit khi `make test` chưa exit 0 trong chính lượt này.

## Lệnh
```sh
git add -A && git status --short
git commit -m "<type>(<scope>): <mô tả>

Implements docs/specs/NNN-....md
Build: clean, ASan+UBSan.
Tests: <tên test> pass."
```

## Quy tắc
- Một spec, một commit. Không gộp hai spec.
- Body phải nêu số spec. Đây là sợi dây duy nhất nối code về thiết kế.
- Không `git push` nếu chưa được duyệt.
```