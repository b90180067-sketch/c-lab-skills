---
name: write-spec
description: Dùng mỗi khi tạo một file mới trong docs/specs/.
---

# write-spec

## Trình tự
1. `ls docs/specs/` để lấy số thứ tự kế tiếp.
2. `rg -l "<khái niệm liên quan>" src/ include/` — liệt kê file đã có.
3. Tra `docs/INDEX.md` → đọc mục tham chiếu tương ứng.
4. Viết file theo đúng 8 mục trong SOUL. Thiếu mục nào là spec hỏng.
5. Tự kiểm bằng checklist dưới trước khi báo xong.

## Checklist tự kiểm
- [ ] Mọi con trỏ trong Interface đã có dòng Ownership tương ứng?
- [ ] Acceptance có phải là một lệnh shell chạy được không?
- [ ] Non-goals có ít nhất hai mục không?
- [ ] Đã nêu ít nhất một phương án bị loại và lý do?
- [ ] Ước lượng < 200 dòng C? Nếu không, đã tách chưa?
- [ ] Có file nào trong "Files touched" chưa tồn tại? Nói rõ là file mới.

## Không được làm
- Viết thân hàm. Chữ ký thì có, thân hàm thì không.
- Dùng "..." hoặc "tương tự" trong phần Interface.
- Để "TBD" ở bất kỳ mục nào. Chưa quyết được thì hỏi người dùng.
```