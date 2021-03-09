# 9.6. range

`range` 模块提供了基于范围的整数迭代器的实现.

## 构造器

模块提供如下构造器, 用于构造 `Range` 迭代器:

* `until(begin: i32, end: i32): Range`: 构造一个可迭代 `[begin, end)` 区间内整数的迭代器.
* `to(begin: i32, end: i32): Range`: 构造一个可迭代 `[begin, end]` 区间内整数的迭代器.

## 方法

`Range` 具备如下方法:

### 迭代器

* `next(): i32`: 迭代器方法, 返回当前迭代的整数, 并切换到下一迭代.
* `last(): bool`: 迭代器方法, 判断当前迭代是否是最后一次迭代.

### 其他

* `step(step: i32): Range`: 根据当前的 `Range` 迭代器, 产生一个其他参数均相同, 但迭代步长为 `step` 的新迭代器.

## 示例

```yu
import io
import range

extern def main(argc: i32, argv: u8**): i32 {
  // 从 1 数到 19
  out <<< "counting..."
  for i in 1 until 20 {
    out <<< ' ' <<< i
  }
  out <<< '\n'

  // 从 10 倒数到 1
  out <<< "countdown!\n"
  for i in 10 to 1 step -1 {
    out <<< i <<< "!\n"
  }
  out <<< "launch!\n"

  0
}
```
