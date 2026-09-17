---
name: new-module
description: Khi tạo file .c hoặc .h mới.
---

# new-module

## Cùng một lượt, đủ bốn việc
1. `include/<name>.h` — header guard `<PROJECT>_<NAME>_H`, include tối thiểu.
2. `src/<name>.c` — include header của chính nó **dòng đầu tiên** (phát hiện
   header thiếu include).
3. Thêm `<name>.o` vào biến OBJS trong Makefile.
4. `tests/test_<name>.c` với ít nhất một case, kể cả trivial.

Thiếu bước 3 hoặc 4 là chưa xong, dù build xanh.

## Khuôn header
```c
#ifndef CLAB_NAME_H
#define CLAB_NAME_H
#include <stddef.h>
/* Ownership: caller owns the returned buffer, free with name_free(). */
...
#endif /* CLAB_NAME_H */
```

## Thứ tự include trong .c
header của chính nó → header hệ thống → header dự án. Đúng thứ tự này.