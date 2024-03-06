**用途：重新启动应用程序后，仍恢复到离开时的状态。**

可以使用 [[归档数据 - Codable|Codable]] 以两种方式之一保存和加载导航栈路径，具体取决于您使用的路径类型：

1. 如果您使用 [[导航路径 - NavigationPath]] 来存储 `NavigationStack` 的活动路径，SwiftUI 提供了两个助手，可以让您更轻松地保存和加载路径。
2. 如果您使用的是同质[[数组 - Array]]，例如 `[Int]` 或 `[String]` ，那么就不需要这些助手，您可以自由加载或保存数据。

两种方法都依赖于外部[[类 - Class]]的自动处理，把**路径**存储在视图之外。

当我们的路径数据存储为**整数**数组时，该类的外观如下：

```swift
@Observable
class PathStore {
    var path: [Int] {
        didSet {
            save()
        }
    }

    private let savePath = URL.documentsDirectory.appending(path: "SavedPath")

    init() {
        if let data = try? Data(contentsOf: savePath) {
            if let decoded = try? JSONDecoder().decode([Int].self, from: data) {
                path = decoded
                return
            }
        }

        // Still here? Start with an empty path.
        path = []
    }

    func save() {
        do {
            let data = try JSONEncoder().encode(path)
            try data.write(to: savePath)
        } catch {
            print("Failed to save navigation data")
        }
    }
}
```

如果您使用的是 `NavigationPath` ，只需做四个小改动：

```swift
@Observable
class PathStore {
    var path: NavigationPath {
        didSet {
            save()
        }
    }

    private let savePath = URL.documentsDirectory.appending(path: "SavedPath")

    init() {
        if let data = try? Data(contentsOf: savePath) {
            if let decoded = try? JSONDecoder().decode(NavigationPath.CodableRepresentation.self, from: data) {
                path = NavigationPath(decoded)
                return
            }
        }

        // Still here? Start with an empty path.
        path = NavigationPath()
    }

    func save() {
        guard let representation = path.codable else { return }

        do {
            let data = try JSONEncoder().encode(representation)
            try data.write(to: savePath)
        } catch {
            print("Failed to save navigation data")
        }
    }
}
```

最后要将 PathStore 绑定：

```swift
struct ContentView: View {
    @State private var pathStore = PathStore()

    var body: some View {
        NavigationStack(path: $pathStore.path) {
            DetailView(number: 0)
                .navigationDestination(for: Int.self) { i in
                    DetailView(number: i)
                }
        }
    }
}
```

[参考链接](https://www.hackingwithswift.com/books/ios-swiftui/how-to-save-navigationstack-paths-using-codable)

#data