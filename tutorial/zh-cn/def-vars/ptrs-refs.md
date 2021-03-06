# 3.2. 指针和引用

羽语言支持定义指针和引用类型的变量.

## 指针

你可以使用 `T*` 表示类型 `T` 的指针类型, 此时, 指针指向的对象是不可变的. 也就是说, 你无法修改对 `T*` 类型的变量解引用之后的内容.

你可以使用 `T var*` 表示一个指向可变对象的指针类型.

```yu
import io

extern def main(argc: i32, argv: u8**): i32 {
  var x = 100

  // 定义一个指向不可变对象的指针
  let ptr: i32* = &x
  out <<< "x = " <<< *ptr <<< '\n'
  // 下一行语句会编译出错
  // (*ptr) = 101

  // 定义一个指向可变对象的指针
  let var_ptr: i32 var* = &x
  (*var_ptr) = 101
  out <<< "x = " <<< x <<< '\n'

  0
}
```

## 引用

和指针类似, 在羽语言中你可以使用 `T&` 或 `T var&` 表示可变或不可变的引用.

在编译器看来, 引用和指针别无二致. 不过, 引用总是会指向一个有效的对象, 并且你可以像操作这个对象本身一样, 直接操作一个引用, 而不需要对其解引用.

```yu
import io

extern def main(argc: i32, argv: u8**): i32 {
  var x = 100

  // 定义不可变引用
  let ref: i32& = x
  out <<< "x = " <<< ref <<< '\n'
  // 下一行语句会编译出错
  // ref = 101

  // 定义可变引用
  let var_ref: i32 var& = x
  var_ref = 101
  out <<< "x = " <<< x <<< '\n'

  0
}
```
