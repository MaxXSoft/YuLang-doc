# 9.8. strview

`strview` 模块提供了对不可变字符串的各类操作, 并将其组织成了 `StrView` 结构的实现.

## 构造器

模块提供如下构造器, 用于构造 `StrView` 对象:

* `newStrView(str: u8*): StrView`: 从空终止字符串 ([null-terminated string](https://en.wikipedia.org/wiki/Null-terminated_string)) 构造一个 `StrView` 对象.
* `newStrView(buf: u8*, len: u32): StrView`: 从字符数组构造一个 `StrView` 对象, `buf` 为字符数组的首地址, `len` 为其长度.

## 方法

`StrView` 具备如下方法:

### 元素访问

* `at(i: i32): u8`/`at(i: u32): u8`: 返回字符串内的第 `i` 个字符.
* `front(): u8`: 返回字符串的第一个字符.
* `back(): u8`: 返回字符串的最后一个字符.
* `str(): u8*`: 返回对象所持有字符串的指针. 此方法不保证返回的指针一定指向一个空终止字符串.

### 迭代器

* `split(delimiter: u8): __StrViewSplitIter`: 以 `delimiter` 字符分割当前对象, 返回一个迭代所有分割后字符串的迭代器.

### 容量

* `empty(): bool`: 测试变长数组是否为空.
* `len(): u32`: 返回对象所持有字符串的长度.

### 元素修改

* `removePrefix(n: i32)`: 删除 `StrView` 开头的 `n` 个字符.
* `removeSuffix(n: i32)`: 删除 `StrView` 结尾的 `n` 个字符.

## 运算符

`StrView` 重载了如下运算符:

* `==(str: u8*): bool`: 判断当前对象和 `str` 所表示的空终止字符串是否相等.
* `!=(str: u8*): bool`: 判断当前对象和 `str` 所表示的空终止字符串是否不等.
* `==(that: StrView&): bool`: 判断当前对象和 `that` 所表示的 `StrView` 对象是否相等.
* `!=(that: StrView&): bool`: 判断当前对象和 `that` 所表示的 `StrView` 对象是否不等.

## 示例

```yu
import io
import strview

// 为 `StrView` 重载流输出运算符
def <<<(this: IO&, sv: StrView&): IO& {
  var i = 0 as u32
  while i < sv.len() {
    this <<< sv.at(i)
    i += 1 as u32
  }
  this
}

extern def main(argc: i32, argv: u8**): i32 {
  // 新建两个 `StrView`
  var sv1 = newStrView("test1")
  var sv2 = newStrView("test2")

  // 输出 `sv1` 和 `sv2` 的内容并判等
  out <<< "sv1: " <<< sv1 <<< ", sv2: " <<< sv2 <<< '\n'
  out <<< "sv1 == sv2? " <<< sv1 == sv2 <<< "\n\n"

  // 删除 `sv1` 和 `sv2` 尾部的字符, 输出修改后的 `StrView` 并判等
  sv1.removeSuffix(1)
  sv2.removeSuffix(1)
  out <<< "removed, sv1: " <<< sv1 <<< ", sv2: " <<< sv2 <<< '\n'
  out <<< "sv1 == sv2? " <<< sv1 == sv2 <<< "\n\n"

  // 使用 `split` 分割 `StrView` 并输出分割后的字符串
  let path = newStrView("~/sam/documents/todo-list.txt")
  out <<< "path:\n"
  for sv in path.split('/') {
    out <<< "  " <<< sv <<< '\n'
  }
  0
}
```
