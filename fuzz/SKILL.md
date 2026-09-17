---
name: fuzz
description: Fuzz lexer, parser, và HTTP request parser.
---

# fuzz

## Dựng harness (một lần cho mỗi target)
```c
/* fuzz/fuzz_parser.c */
#include <stdint.h>
#include <stddef.h>
int LLVMFuzzerTestOneInput(const uint8_t *d, size_t n) {
    parse_source((const char *)d, n);   /* không assert, chỉ chạy */
    return 0;
}
```

## Chạy
```sh
clang -g -O1 -fsanitize=fuzzer,address,undefined \
  fuzz/fuzz_parser.c compiler/*.c -Icompiler -o /tmp/fuzz_parser
/tmp/fuzz_parser corpus/ -max_total_time=600 -seed=1337 -print_final_stats=1
```

## Quy tắc
- **Luôn ghi lại seed.** `-seed=1337`. Crash không tái hiện được không
  phải finding.
- Crash file rơi vào `crash-<hash>`. Copy vào `corpus/crashes/` và ghi
  đường dẫn vào finding.
- Chạy lại crash một lần: `/tmp/fuzz_parser crash-abc123` — phải chết
  lại. Không chết lại thì là flake, ghi vào mục unconfirmed.
- Corpus seed lấy từ file test hợp lệ có sẵn. Fuzz từ corpus rỗng phí
  nửa thời gian để học cú pháp.
```