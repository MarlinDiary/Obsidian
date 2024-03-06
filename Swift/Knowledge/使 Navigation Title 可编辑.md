在使用 .inline 模式显示标题时，可以将[[双向绑定|绑定]]传递给 navigationTitle：

```swift
struct ContentView: View {
    @State private var title = "SwiftUI"

    var body: some View {
        NavigationStack {
            Text("Hello, world!")
                .navigationTitle($title)
                .navigationBarTitleDisplayMode(.inline)
        }
    }
}
```

这样用户就可以自主修改标题了。

#swiftui 