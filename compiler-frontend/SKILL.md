---
name: compiler-frontend
description: Khi làm lexer, parser, hoặc AST.
---

# compiler-frontend

## Tham chiếu
`docs/ref/crafting-interpreters/` phần scanner và compiler. Đọc trước,
đừng dựng lại từ trí nhớ.

## Lexer
- Table-driven hoặc switch lớn, không regex.
- Token giữ con trỏ + độ dài vào source buffer, **không copy chuỗi**.
- Mỗi token mang line và column. Thêm sau thì rất đau.
- EOF là một token thật, không phải NULL.

## Parser
- Recursive descent. Precedence climbing cho biểu thức.
- Error recovery: đồng bộ tại `;` và `}`. Không dừng ở lỗi đầu tiên.
- AST node cấp phát từ arena (`arena.c`). Không free lẻ.
- Mỗi node giữ span (start, end) để báo lỗi chỉ đúng chỗ.

## Test bắt buộc
Mỗi construct mới cần ba test: hợp lệ, sai cú pháp, và rỗng/biên.
```