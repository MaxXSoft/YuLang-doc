# 6.1. 定义结构体

羽语言中结构体的概念和 C/C++ 基本一致. 你可以使用 `struct` 关键字来定义一个结构体:

```yu
import io
import range

// 结构体中的字段使用逗号分隔
struct ClassInfo {
  name: u8*,
  credit: i32,
  class_hours: i32,
}

extern def main(argc: i32, argv: u8**): i32 {
  let classes = [ClassInfo[5]] {
    // 结构体使用与数组相同的初始化语法
    [ClassInfo] {"Data Structure", 3, 54},
    [ClassInfo] {"Algorithm Design and Analysis", 5, 68},
    [ClassInfo] {"Compiler Principles", 4, 85},
    [ClassInfo] {"Introduction to Computer Systems", 5, 68},
    [ClassInfo] {"Computer Architectures", 3, 48},
  }

  for i in 0 until 5 {
    // 使用 `.` 来访问结构体中的字段
    out <<< "class name: " <<< classes[i].name <<< '\n'
    out <<< "  credit: " <<< classes[i].credit <<< '\n'
    out <<< "  class hours: " <<< classes[i].class_hours <<< '\n'
  }
  0
}
```
