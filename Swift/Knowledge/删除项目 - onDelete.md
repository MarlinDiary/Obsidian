SwiftUI 为我们提供了 `onDelete()` [[修改器 - Modifier]]。在实践中，这几乎只与 [[列表 - List]] 和 [[循环视图 - ForEach]] 一起使用。我们创建了一个行 List，使用 ForEach 显示这些行，然后将 `onDelete()` 附加到 `ForEach` 上，这样用户就可以删除他们不想要的行。

`onDelete()` 修改器只存在于 `ForEach` 中，这意味着在只有动态行（List 中的一个概念）的情况下，我们需要编写少量的额外代码，但从另一个角度看，这也意味着我们可以更轻松地创建只能删除部分行的列表。

为了使 `onDelete()` 正常工作，我们需要一个方法，该方法将接收一个类型为 `IndexSet` 的参数。这有点像一组整数，只不过它是排序过的，而且它只是告诉我们 `ForEach` 中所有应删除项目的位置。

由于我们的 `ForEach` 完全是由一个[[数组 - Array]]创建的，因此我们实际上可以直接将 index set 传递给那个数组。数组有一个特殊的 `remove(atOffsets:)` 方法，可以接受 index set。

```swift
func removeRows(at offsets: IndexSet) {
    arrayName.remove(atOffsets: offsets)
} 
```

当 SwiftUI 想要删除 `ForEach` 中的数据时，我们可以通过以下内容来调用该方法：

```swift
ForEach(numbers, id: \.self) {
    Text("Row \($0)")
}
.onDelete(perform: removeRows)
```

当 `.onDelete(perform:)` 被触发时，SwiftUI自动将包含了被选中以删除的行的索引的 `IndexSet` 传递给 `removeRows` 方法。

SwiftUI 还有个窍门：在导航栏上添加一个 "编辑/完成 "按钮，让用户可更轻松地删除几行：

```swift
.toolbar {
    EditButton()
}
```

#swiftui 