# 9.1. sys

`sys` 是一个模块集合, 其中包含了若干模块, 这些模块内都声明了部分 C 语言标准库中的函数, 或部分 POSIX API:

* `ctype`: 声明了 `ctype.h` 中的函数;
* `math`: 声明了 `math.h` 中的**部分**函数;
* `stdlib`: 声明了 `stdlib.h` 中的**部分**函数;
* `string`: 声明了 `string.h` 中的**部分**函数;
* `unistd`: 声明了 `unistd.h` 中的**部分** POSIX API.

可用的函数声明请参考相关文件的源码.

## 示例

```yu
import io
import sys.stdlib

extern def main(argc: i32, argv: u8**): i32 {
  // `seed` 函数并非 C 语言标准库函数, 它是一个定义在 `sys.stdlib` 中的内联函数
  // 可使用 `srand` 和当前时间初始化随机数种子, 并将种子返回
  seed()

  out <<< "rand #1: " <<< rand() <<< '\n'
  out <<< "rand #2: " <<< rand() <<< '\n'
  out <<< "rand #3: " <<< rand() <<< '\n'
  out <<< "rand #4: " <<< rand() <<< '\n'
  out <<< "rand #5: " <<< rand() <<< '\n'
  0
}
```
