当我们使用 [[列表 - List]] 或[[循环视图 - ForEach]] 制作动态视图时，SwiftUI 需要知道如何才能唯一地识别每个项目，否则它将很难比较视图层次结构来找出发生了哪些变化。

我们可以通过以下方式自动生成 UUID ：

```swift
struct ExpenseItem {
    let id = UUID()
    let name: String
    let type: String
    let amount: Int
}
```

#swiftui #function 