---
name: debug-c
description: Khi segfault, sai kết quả, hoặc ASan báo lỗi.
---

# debug-c

## Thứ tự, không đảo
1. Tái hiện. Một lệnh, chạy lại được. Chưa tái hiện được thì chưa debug.
2. Chạy dưới ASan trước gdb. ASan chỉ thẳng chỗ hỏng, gdb chỉ chỗ chết.
3. `gdb --args ./prog ...` → `run` → `bt full` → `p *ptr` ở frame nghi ngờ.
4. Thu hẹp bằng cách xoá bớt input, không bằng cách thêm printf.

## Quy tắc
- Không sửa khi chưa biết **vì sao** hỏng. "Thêm check NULL thì hết crash"
  không phải chẩn đoán, đó là giấu triệu chứng.
- Nói lại nguyên nhân bằng một câu trước khi sửa. Không nói được thì chưa hiểu.
- Sửa xong phải có test tái hiện đúng bug đó. Không test thì chưa xong.
```