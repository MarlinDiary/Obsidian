当使用 `@Query` 从 [[SwiftData 框架]] 中提取对象时，您可以指定数据的排序方式。

对排序的描述有两种方式，一种是只允许使用**一个**排序字段的简单选项，另一种是允许使用名为 `SortDescriptor` 的新类型的**数组**的高级版本。

## 简单版本

可能是这样的：

```swift
@Query(sort: \Book.title) var books: [Book]
```

也可以 **reverse** 排序：

```swift
@Query(sort: \Book.rating, order: .reverse) var books: [Book]
```

## 高级版本

我们可以在 SortDescriptor 中只提及想要排序的**属性**：

```swift
@Query(sort: [SortDescriptor(\Book.title)]) var books: [Book]
```

也可以对默认的升序进行**反转**：

```swift
@Query(sort: [SortDescriptor(\Book.title, order: .reverse)]) var books: [Book]
```

最重要的是，我们可以添加**多个**排序条件：

```swift
@Query(sort: [
    SortDescriptor(\Book.title),
    SortDescriptor(\Book.author)
]) var books: [Book]
```

#data #hard 