您已经看到 [[列表 - List]] 和[[表单 - Form]] 是如何让我们创建滚动数据表的，但当我们想要滚动任意数据（即我们手工创建的一些视图）时，我们需要使用 SwiftUI 的 `ScrollView` 。

滚动视图可以水平、垂直滚动，你还可以控制系统是否应该在它们旁边显示滚动指示器。

我们可以创建一个包含 100 个文本视图的滚动列表：

```swift
ScrollView {
    VStack(spacing: 10) {
        ForEach(0..<100) {
            Text("Item \($0)")
                .font(.title)
        }
    }
}
```

要想获得整个区域都可以滚动的效果，我们应该让 `VStack` 占用更多空间，同时保留默认的居中对齐方式：

```swift
ScrollView {
    VStack(spacing: 10) {
        ForEach(0..<100) {
            Text("Item \($0)")
                .font(.title)
        }
    }
    .frame(maxWidth: .infinity)
}
```

使用`ScrollView`时，所有的视图元素都会同时加载到内存中，这可能会影响性能，如果你想避免这种情况发生， [[堆栈 - Stack]]中的`VStack` 和 `HStack` 都有一个替代方案，分别称为 `LazyVStack` 和 `LazyHStack` 。它们的使用方式与普通堆栈完全相同，但会**按需加载内容**。

另外，在制作 `ScrollView` 时，将 `.horizontal` 作为参数传递，即可制作**水平**滚动视图：

```swift
ScrollView(.horizontal) {
    LazyHStack(spacing: 10) {
        ForEach(0..<100) {
            CustomText("Item \($0)")
                .font(.title)
        }
    }
}
```

## 修饰符

| 修饰符 | 作用 |
| ---- | ---- |
| .showsIndicators: **false** | 控制滚动视图的滚动条（指示器）是否显示 |
|  |  |

#swiftui 