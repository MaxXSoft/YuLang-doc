# 8.4. 迭代器

羽语言中, `for-in` 循环用于遍历一个迭代器对象. 而此处的 “迭代器对象”, 实际上是指一个具备 `next` 方法和 `last` 方法的 “对象”.

不要被 “对象” 这个词所迷惑, 还记得我们之前提过的 “点函数调用” 语法吗? 所谓的 “方法”, 实际上就是一个点函数, 即具备至少一个参数的函数; 而对象, 不过指的是传入点函数的第一个实参.

## 迭代器方法

`next` 和 `last` 方法除需要将对象本身作为参数传入以外, 不需要具备任何其他参数. `next` 方法必须具备返回值, 返回值的类型不限; 而 `last` 方法必须具备一个 `bool` 类型的返回值.

顾名思义, 迭代器的 `next` 方法会返回本次迭代的值, 并切换到下一次迭代; `last` 方法用于判断迭代器是否已经进行到了最后一次迭代.

## for-in 循环的工作流程

对于以下的 `for-in` 循环:

```yu
for i in iter {
  use(i)
}
```

其工作流程等价于以下的伪代码描述:

```
var iter' = iter
while not iter'.last() {
  let i = iter'.next()
  use(i)
}
```

注意, 迭代器对象的 `next` 方法可能会返回一个引用, 此时 `i` 也会是一个相同的引用, 而非一个引用的拷贝.

也就是说, 如果 `next` 方法返回了一个可变引用, 那么你可以通过修改 `i` 来修改这个引用指向的对象; 否则, 你不能对 `i` 进行任何更改, 因为 `i` 是不可变的.

## 示例

```yu
import io

// 数组迭代器
// 用于迭代一个 `i32` 整数数组
// 迭代时可以修改数组中的元素
struct ArrayIter {
  arr: i32 var*,
  len: u32,
  cur: u32,
}

def newArrayIter(arr: i32 var*, len: u32): ArrayIter {
  [ArrayIter] {arr, len, 0 as u32}
}

def next(this: ArrayIter var&): i32 var& {
  var cur: i32 var& = this.arr[this.cur]
  this.cur += 1 as u32
  cur
}

def last(this: ArrayIter&): bool {
  this.cur >= this.len
}

extern def main(argc: i32, argv: u8**): i32 {
  let len = 5 as u32
  var arr = [i32[len]] {1, 2, 3, 4, 5}

  // 使用数组迭代器为数组的每一个元素乘二
  for i in newArrayIter(arr as i32 var*, len) {
    i *= 2
  }

  // 使用数组迭代器遍历输出数组内的每一个元素
  out <<< "arr = { "
  for i in newArrayIter(arr as i32 var*, len) {
    out <<< i <<< ' '
  }
  out <<< "}\n"
  0
}
```
