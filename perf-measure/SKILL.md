---
name: perf-measure
description: Chỉ dùng khi người dùng hỏi về hiệu năng. Không tự chạy.
---

# perf-measure

## Quy tắc số một
Không nói gì về hiệu năng khi chưa đo. Suy đoán về tốc độ là điều
duy nhất bị cấm tuyệt đối trong bot này.

## Lệnh
```sh
make clean && make CFLAGS="-std=c11 -O2 -g"
perf stat -r 10 ./prog <input>
perf record -g ./prog <input> && perf report --stdio | head -30
```

## Báo cáo
Luôn kèm: lệnh, số lần lặp, độ lệch chuẩn, và phần trăm thời gian của
ba hàm đầu. Một con số đơn lẻ không có độ lệch là vô nghĩa.
```