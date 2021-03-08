# 8.3. 点函数

在羽语言中, 形如 `func(a1, a2, a3, ..., an)` 的函数调用, 均可被写作 `a1.func(a2, a3, ..., an)`, 这种写法被称作 “点函数调用”.

```yu
import io

def iif(cond: bool, tval: i32, fval: i32): i32 {
  if cond { tval } else { fval }
}

def toUpper(c: u8): u8 {
  if c >= 'a' && c <= 'z' {
    c - 'a' + 'A'
  }
  else {
    c
  }
}

extern def main(argc: i32, argv: u8**): i32 {
  // 以下这些写法都是等价的
  let iif1 = iif(argc > 1, 1, 2)
  let iif2 = (argc > 1).iif(1, 2)

  let to_upper1 = toUpper('s')
  let to_upper2 = 's'.toUpper()

  out <<< "iif1 == iif2?           " <<< iif1 == iif2 <<< '\n'
  out <<< "to_upper1 == to_upper2? " <<< to_upper1 == to_upper2 <<< '\n'
  0
}
```

借助点函数的语法, 以及函数重载的特性, 我们可以很方便地将程序写成如 C++, Java 等面向对象编程语言的风格.

```yu
import io

struct Student {
  name: u8*,
  age: i32,
  graduated: bool,
}

// 构造一个 `Student` 对象
def newStudent(name: u8*, age: i32, graduated: bool): Student {
  [Student] {name, age, graduated}
}

// 构造一个 `Student` 对象, 只需提供 `name` 字段
def newStudent(name: u8*): Student {
  [Student] {name, -1, false}
}

// 对象的一些方法
def setAge(this: Student var&, age: i32) {
  this.age = age
}

def selfIntro(this: Student&) {
  out <<< "Hello, my name is " <<< this.name <<< ", " <<<
          "I'm " <<< this.age <<< " years old, " <<<
          "and I " <<< if this.graduated {
                           "have graduated"
                         }
                         else {
                           "haven't graduated yet"
                         } <<< ".\n"
}

extern def main(argc: i32, argv: u8**): i32 {
  // 创建两个学生对象
  let student1 = newStudent("Accelerator", 16, true)
  var student2 = newStudent("Misaka Mikoto")

  // 修改第二个学生的年龄
  student2.setAge(14)

  // 自我介绍
  student1.selfIntro()
  student2.selfIntro()
  0
}
```

这种写法在羽语言编写的程序中十分常见.
