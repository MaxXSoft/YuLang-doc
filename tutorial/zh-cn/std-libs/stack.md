# 9.7. stack

`stack` 模块提供了栈容器的实现. 由于羽语言暂不支持泛型, 该栈内仅能存储 `u8 var*` 类型数据.

## 构造器

模块提供如下构造器, 用于构造 `Stack` 对象:

* `newStack(): Stack`: 构造一个新的栈对象.

## 方法

`Stack` 具备如下方法:

### 析构

* `del()`: 析构当前对象.

### 元素访问

* `top(): u8 var* var&`: 返回栈顶元素的可变引用.

### 容量

* `empty(): bool`: 测试栈是否为空.

### 元素修改

* `clear()`: 清空栈.
* `push(data: u8 var*)`: 将 `data` 推入栈尾部.
* `pop(): u8 var*`: 从栈尾部弹出一个元素并返回.

## 示例

```yu
import io
import stack

extern def main(argc: i32, argv: u8**): i32 {
  // 新建一个栈并推入一些数据
  var s = newStack()
  s.push("test1" as () as u8 var*)
  s.push("test2" as () as u8 var*)
  s.push("test3" as () as u8 var*)

  // 测试栈是否为空
  out <<< "empty? " <<< s.empty() <<< '\n'

  // 访问并修改栈顶的数据
  out <<< "top = " <<< s.top() as u8* <<< '\n'
  s.top() = "test4" as () as u8 var*
  out <<< "top = " <<< s.top() as u8* <<< '\n'

  // 从栈内依次弹出所有数据并输出
  while !s.empty() {
    out <<< s.pop() <<< '\n'
  }

  // 析构栈
  s.del()
  0
}
```
