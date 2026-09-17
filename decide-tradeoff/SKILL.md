---
name: decide-tradeoff
description: Khi có từ hai phương án kiến trúc trở lên.
---

# decide-tradeoff

## Bảng bắt buộc
| Phương án | Dòng code ước tính | Ai đọc cũng hiểu? | Sai ở đâu thì chết? | Đổi về sau tốn gì? |

## Tiêu chí xếp hạng, theo thứ tự ưu tiên
1. Sai lầm có bị compiler bắt không, hay phải chạy mới lộ?
2. Người mới đọc trong 10 phút có hiểu không?
3. Số dòng code.
4. Hiệu năng. **Chỉ** khi có số đo, không được suy đoán.

## Quy tắc
Hiệu năng không bao giờ thắng ba tiêu chí trên nếu chưa profile. Nếu
định viện dẫn hiệu năng, phải kèm lệnh đo và con số, hoặc rút lại.
```