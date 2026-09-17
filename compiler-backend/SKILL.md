---
name: compiler-backend
description: Khi làm IR, register allocation, hoặc sinh mã.
---

# compiler-backend

## Tham chiếu
`docs/ref/sysv-abi.pdf` §3.2 cho quy ước gọi hàm. Mọi câu về thanh ghi
nào caller-saved phải tra ở đây, không đoán.

## Quy tắc
- IR trước, asm sau. Không sinh asm thẳng từ AST.
- Mỗi lệnh IR in ra được dạng text, và có flag `--emit-ir` để dump.
  Đây là công cụ debug quan trọng nhất của cả backend.
- Stack frame align 16 byte trước mỗi `call`. Quên là crash khó hiểu.
- Test codegen bằng cách chạy chương trình sinh ra và so exit code,
  không bằng cách so chuỗi asm.

## Khi output sai
`--emit-ir` trước. Nếu IR đúng mà asm sai, lỗi ở codegen. Nếu IR đã sai,
đừng động vào codegen.
```