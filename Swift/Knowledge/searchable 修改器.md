可以使用 `searchable()` 修改器在视图中添加搜索栏，并将一个字符串属性绑定到搜索栏，以便在用户键入时过滤数据。

一个例子如下：

```swift
struct ContentView: View {
    @State private var searchText = ""

    var body: some View {
        NavigationStack {
            Text("Searching for \(searchText)")
                .searchable(text: $searchText, prompt: "Look for something")
                .navigationTitle("Searching")
        }
    }
}

// 需要确保您的视图位于 NavigationStack 内，否则 iOS 将无处放置搜索框
```

在实践中，`searchable()` 最好与某种数据筛选一起使用。当 `@State` 属性发生变化时，SwiftUI 将重新激活 body 属性，因此可以使用计算属性来处理实际的筛选：

```swift
struct ContentView: View {
    @State private var searchText = ""
    let allNames = ["Subh", "Vina", "Melvin", "Stefanie"]

    var filteredNames: [String] {
        if searchText.isEmpty {
            allNames
        } else {
            allNames.filter { $0.localizedStandardContains(searchText) }
        }
    }

    var body: some View {
        NavigationStack {
            List(filteredNames, id: \.self) { name in
                Text(name)
            }
            .searchable(text: $searchText, prompt: "Look for something")
            .navigationTitle("Searching")
        }
    }
}

// localizedStandardContains() 是根据用户输入进行搜索的最佳方式，它会自动忽略大小写和重音
```

#swiftui 