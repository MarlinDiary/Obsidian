程序化导航允许我们使用代码从一个视图移动到另一个视图，而不是[[导航链接 - NavigationLink|等待用户进行特定操作]]。

这是通过将 `NavigationStack` 的路径[[双向绑定]]到一个数组来实现的：

```swift
struct ContentView: View {
    @State private var path = [Int]()

    var body: some View {
        NavigationStack(path: $path) {
            VStack {
                // more code to come
            }
            .navigationDestination(for: Int.self) { selection in
                Text("You selected \(selection)")
            }
        }
    }
}
```

1. 它创建了一个 `@State` 属性，用于存储整数数组。
2. 它将该属性绑定到 `NavigationStack` 的 `path` 上，这意味着更改数组将自动导航到数组中的任何内容，而且当用户按下导航栏中的 "Back "键时，也会更改数组。

#swiftui #hard 