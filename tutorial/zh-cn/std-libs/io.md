# 9.4. io

`io` 模块提供了对标准输入/输出/错误设备的流式访问接口.

## 常量定义

标准输入/输出/错误流分别被定义为 `iin`, `out`, `err` 三 `IO` 个类型的常量.

## 方法

`IO` 具备如下方法:

* `put(char: u8)`: 向 `IO` 对应的流输出字符 `char`.
* `get(): u8`: 从 `IO` 对应的流中读取一个字符并返回.

## 运算符

`IO` 定义了如下运算符:

### 流输出运算符 `<<<`

* `<<<(str: u8*): IO&`: 向流输出字符串 `str`.
* `<<<(char: u8): IO&`: 向流输出字符 `char`.
* `<<<(uint: usize): IO&`: 向流输出指针宽度无符号整数 `uint`.
* `<<<(uint: u32): IO&`: 向流输出 32 位无符号整数 `uint`.
* `<<<(int: i32): IO&`: 向流输出 32 位有符号整数 `int`.
* `<<<(val: bool): IO&`: 向流输出布尔值 `val`.

### 流输入运算符 `>>>`

* `>>>(char: u8 var&): IO&`: 从流中读取字符并存储到 `char` 中.
* `>>>(uint: usize var&): IO&`: 从流中读取指针宽度无符号整数并存储到 `uint` 中.
* `>>>(uint: u32 var&): IO&`: 从流中读取 32 位无符号整数并存储到 `uint` 中.
* `>>>(int: i32 var&): IO&`: 从流中读取 32 位有符号整数并存储到 `int` 中.

## 示例

```yu
import io

extern def main(argc: i32, argv: u8**): i32 {
  // 输出数据
  out <<< "Hello world!\n"
  out <<< "1 + 2 = " <<< 1 + 2 <<< '\n'
  out <<< "3 == 1? " <<< 3 == 1 <<< '\n'

  // 读取数据
  var i: i32
  out <<< "input an integer i: "
  iin >>> i
  out <<< "i * 3 = " <<< i * 3 <<< '\n'
  0
}
```
