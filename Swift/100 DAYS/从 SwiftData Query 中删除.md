对于已经放入 [[列表 - List]] 中的 @Query [[SwiftData 框架]] 对象，只需一点额外的工作，就可以实现滑动删除的效果。

与常规数据数组一样，大部分工作都是通过在 [[循环视图 - ForEach]] 中附加 [[删除项目 - onDelete|onDelete(perform:)]] 修饰符来完成的。

但我们还需要在查询（Query）中找到请求的对象，然后在 Model Context 中调用 `delete()` ，而不是直接从数组中删除项目。

1. 首先，将此方法添加到 `ContentView` 中。

```swift
func deleteBooks(at offsets: IndexSet) {
    for offset in offsets {
        // find this book in our query
        let book = books[offset]

        // delete it from the context
        modelContext.delete(book)
    }
}
```

2. 我们可以通过在 `ForEach` 中添加 `onDelete(perform:)` 修饰符来触发该功能，但请记住：它必须位于 `ForEach` 中，而不是 `List` 中。

```swift
.onDelete(perform: deleteBooks)
```

3. 我们还可以通过添加一个编辑/完成按钮来做得更好。

```swift
ToolbarItem(placement: .topBarLeading) {
    EditButton()
}

//放在 toolbar 修饰符中
```

#data 