# 9.3. hashmap

`hashmap` 模块提供了哈希图的实现. 由于羽语言暂不支持泛型, 该哈希图仅能存储 `(i32, u8 var*)` 键值对.

## 类型定义

模块提供了如下的类型定义:

* `type HashFunc = (HashMap var&, u32): u32`: `key` 的哈希函数. 第一个参数为哈希表的引用, 第二个参数为 `key`, 返回哈希后的 `key`.

## 构造器

模块提供如下构造器, 用于构造 `HashMap` 对象:

* `newHashMap(): HashMap`: 构造一个新的哈希图对象.
* `newHashMap(hash_func: HashFunc): HashMap`: 构造一个新的哈希图对象, 并指定 `key` 的哈希函数.

## 方法

`HashMap` 具备如下方法:

### 析构

* `del()`: 析构当前对象.

### 元素访问

* `get(key: u32): u8 var*`: 查找并返回哈希图中键为 `key` 的元素, 如果找不到则返回 `null`.

### 迭代器

* `iter(): __KvPairTableIter`: 返回哈希图的键值对迭代器 (不可变).

迭代时, 元素的类型为 `__KeyValye`, 其具备两个方法:

* `key(): u32`: 返回当前键值对的键.
* `value(): u8 var*`: 返回当前键值对的值.

### 容量

* `empty(): bool`: 测试哈希表是否为空.
* `size(): u32`: 返回哈希表中键值对的个数.

### 元素修改

* `clear()`: 清空哈希图.
* `insert(key: u32, value: u8 var*): bool`: 向哈希图中插入键值对 `(key, value)`, 成功时返回 `true`.
* `remove(key: u32): bool`: 从哈希图中删除键值对 `(key, _)`, 成功时返回 `true`.

## 示例

```yu
import io
import hashmap

def insert(this: HashMap var&, key: i32, value: u8*): bool {
  this.insert(key as u32, value as () as u8 var*)
}

def get(this: HashMap var&, key: i32): u8* {
  this.get(key as u32)
}

def remove(this: HashMap var&, key: i32): bool {
  this.remove(key as u32)
}

// 输出哈希图的内容
def print(this: HashMap&) {
  out <<< "size: " <<< this.size() <<< '\n'
  out <<< "contents:\n"
  for kv in this.iter() {
    out <<< "  " <<< kv.key() <<< " -> " <<< kv.value() <<< '\n'
  }
  out <<< '\n'
}

extern def main(argc: i32, argv: u8**): i32 {
  // 新建一个哈希图
  var map = newHashMap()

  // 插入键值对, 输出哈希图的内容
  map.insert(1, "test1")
  map.insert(3, "test3")
  map.insert(100, "test100")
  map.insert(33, "test33")
  map.insert(42, "test42")
  map.print()

  // 删除一个键值对
  map.remove(3)
  out <<< "removed #3\n"
  map.print()

  // 访问键值对
  out <<< "#42 = " <<< map.get(42) <<< '\n'

  // 析构哈希图
  map.del()
  0
}
```
