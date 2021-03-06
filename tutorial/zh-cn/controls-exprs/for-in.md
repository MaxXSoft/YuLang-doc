# 4.5. for-in

`for-in` 语句可用来遍历一个迭代器对象.

在羽语言的标准库中, 很多地方都使用了迭代器, 比如 `range`. `range` 可用来枚举某个范围内的整数:

```yu
import io
import range

extern def main(argc: i32, argv: u8**): i32 {
  let numbers = [i32[5]] {12, 450, 1919, 42, 810}

  // 借助 `range` 遍历数组
  out <<< "my favorite numbers: "
  for i in 0 until 5 {
    out <<< numbers[i] <<< ' '
  }
  out <<< '\n'

  0
}
```

关于迭代器的相关内容, 请参考 [8.4 节](sugars/iterators.md).
