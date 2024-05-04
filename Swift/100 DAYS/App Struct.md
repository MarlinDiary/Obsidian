每个项目都有一个这样的[[结构 - Struct]]，它是我们正在运行的整个应用程序的启动平台。

```swift
import SwiftUI

@main
struct BookwormApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```

1. `@main` 告诉 Swift 这将启动我们的应用程序。从内部来讲，当用户从 iOS 主屏幕启动我们的应用程序时，它将引导整个程序。

2. `WindowGroup` 部分告诉 SwiftUI，我们的应用程序可以在多个窗口中显示。这在 iPhone 上作用不大，但在 iPad 和 macOS 上就变得非常重要了。

#struct 