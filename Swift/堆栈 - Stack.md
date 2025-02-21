如果我们想返回多个内容，我们有多种选择，但有三个选择特别有用。它们是 `HStack` 、 `VStack` 和 `ZStack` ，分别用于处理水平、垂直和纵深。

如果我们想返回两个一上一下的文本视图，可以这样写：

```swift
var body: some View {
    Text("Hello, world!")
    Text("This is another text view")
}
```

但我们也可以这样写：

```swift
var body: some View {
    VStack {
        Text("Hello, world!")
        Text("This is inside a stack")
    }
}
```

这里的结果是一样的，但有三个重要的不同点：

1. 通过明确的方式，我们可以指定在视图之间留出多少空间；
2. 它还允许我们指定对齐方式--视图应该放在彼此的左边、右边还是中间；
3. 如果我们没有明确要求垂直堆叠，SwiftUI 可以自由地以不同的方式排列这些视图--如果它们位于使用水平放置的更大视图中，它们也可能以水平方式显示。

## Spacing 和 Alignment

默认情况下， `VStack` 会在**内部**的两个视图之间自动设置一定的间距，但我们可以在创建堆栈时提供一个参数来控制间距，就像这样：

```swift
VStack(spacing: 20) {
    Text("Hello, world!")
    Text("This is inside a stack")
}
```

默认情况下， `VStack` 将视图居中对齐，但您可以使用其 `alignment` 属性进行控制：

```swift
VStack(alignment: .leading) {
    Text("Hello, world!")
    Text("This is inside a stack")
}
```

除了 `VStack` 之外，我们还有用于水平排列的 `HStack` 。其语法与 `VStack` 相同，包括添加间距和对齐方式。

`ZStack` 没有 Spacing 的概念，因为视图是重叠的，但它有 Alignment 的概念。

## Spacer()

如果在 `VStack` 末尾添加一个 Spacer 视图，就会将所有视图推到屏幕顶部：

```swift
VStack {
    Text("First")
    Text("Second")
    Text("Third")
    Spacer()
}
```

如果您添加了多个 Spacer，它们将分割它们之间的可用空间：

```swift
VStack {
    Spacer()
    Text("First")
    Text("Second")
    Text("Third")
    Spacer()
    Spacer()
}
```

#swiftui #struct #easy 