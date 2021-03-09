# 9.5. queue

`queue` 模块提供了链式队列容器的实现. 由于羽语言暂不支持泛型, 该队列仅能存储 `i32` 类型数据.

## 构造器

模块提供如下构造器, 用于构造 `Queue` 对象:

* `newQueue(): Queue`: 构造一个新的队列对象.

## 方法

`Queue` 具备如下方法:

### 析构

* `del()`: 析构当前对象.

### 容量

* `empty(): bool`: 测试队列是否为空.

### 元素修改

* `push(val: i32)`: 将 `val` 放入队列尾部.
* `pop(): i32`: 从变长数组头部弹出一个元素并返回.

## 示例

```yu
import io
import queue

extern def main(argc: i32, argv: u8**): i32 {
  // 新建一个队列
  var q = newQueue()

  // 向其中推入三个元素
  q.push(1)
  q.push(2)
  q.push(3)

  // 弹出并输出队列中的所有元素
  while !q.empty() {
    out <<< q.pop() <<< '\n'
  }

  // 析构队列
  q.del()
  0
}
```
