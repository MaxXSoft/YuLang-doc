# 9.2. dynarray

`dynarray` 模块提供了变长数组容器的实现. 由于羽语言暂不支持泛型, 该变长数组仅能存储 `i32` 类型数据.

## 构造器

模块提供如下构造器, 用于构造 `DynArray` 对象:

* `newDynArray(): DynArray`: 构造一个新的变长数组对象.
* `newDynArray(count: usize, data: i32): DynArray`: 构造一个新的变长数组对象, 将其长度初始化为 `count`, 所有元素均填充为 `data`.

## 方法

`DynArray` 具备如下方法:

### 析构和复制

* `del()`: 析构当前对象.
* `clone(): DynArray`: 复制当前对象, 并返回复制后的新对象.

### 元素访问

* `get(index: i32): i32`: 读取数组内的第 `index` 个元素.
* `set(index: i32, data: i32)`: 将数组内的第 `index` 个元素写入为 `data`.
* `front(): i32`: 返回数组的第一个元素.
* `back(): i32`: 返回数组的最后一个元素.
* `data(): i32 var*`: 返回变长数组所持有的数组数据.

### 迭代器

* `iter(): __DynArrayIter`: 返回变长数组的不可变迭代器.

### 容量

* `empty(): bool`: 测试变长数组是否为空.
* `size(): usize`: 返回变长数组中元素的个数.
* `capacity(): usize`: 返回变长数组的容量, 即变长数组所持有的数组数据中实际可存放多少元素.

### 元素修改

* `clear()`: 清空变长数组.
* `push(data: i32)`: 将 `data` 放入变长数组尾部.
* `pop(): i32`: 从变长数组尾部弹出一个元素并返回.
* `resize(size: usize, data: i32)`: 重设变长数组中的元素个数. 如果 `size` 小于实际的元素个数, 则将数组尾部多余的元素舍去; 否则, 在尾部补充若干个 `data`.
* `resize(size: usize)`: 同 `resize`. 如果 `size` 大于实际的元素个数, 在尾部补充若干个 0.
* `map(op: (i32): i32)`: 对数组内的元素统一应用 `op` 操作.
* `reduce(op: (i32, i32): i32): i32`: 从左至右, 依次对数组元素执行 `reduce` 操作.

## 运算符

`DynArray` 重载了如下运算符:

* `=(that: DynArray&)`: 将当前对象的内容拷贝为 `that` 的内容.

## 示例

```yu
import range
import io
import dynarray

def addOne(val: i32): i32 {
  val + 1
}

def add(l: i32, r: i32): i32 {
  l + r
}

// 输出数组的内容
def print(this: DynArray&) {
  out <<< "content of array: "
  for i in this.iter() {
    out <<< i <<< ' '
  }
  out <<< '\n'
}

extern def main(argc: i32, argv: u8**): i32 {
  // 新建一个动态数组, 并向其中放入四十个元素
  var arr = newDynArray()
  for i in 0 until 40 {
    arr.push(i)
  }

  // 输出数组内容
  arr.print()

  // 执行一些操作
  out <<< "adding one...\n"
  arr.map(addOne)
  arr.print()
  out <<< "sum: " <<< arr.reduce(add) <<< '\n'
  out <<< "size: " <<< arr.size()
  out <<< ", capacity: " <<< arr.capacity() <<< '\n'

  // 析构数组
  arr.del()
  0
}
```
