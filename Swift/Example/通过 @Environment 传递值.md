如果需要在应用程序中的多个地方共享同一个对象，我们可以求助于 SwiftUI 的 Environment。

首先，以下代码将创建一个可以被 SwiftUI 观察到的 `Player` 类：

```swift
@Observable
class Player {
    var name = "Anonymous"
    var highScore = 0
}
```

然后，我们就可以在这样一个小视图中显示他们的高分：

```swift
struct HighScoreView: View {
    var player: Player

    var body: some View {
        Text("Your high score: \(player.highScore)")
    }
}
```

接着我们可以编写这样的代码：

```swift
struct ContentView: View {
    @State private var player = Player()

    var body: some View {
        VStack {
            Text("Welcome!")
            HighScoreView(player: player)
        }
    }
}
```

以上代码显示了直接将值传递到子视图，因此可以在子视图中使用。

但通常情况下，我们有更复杂的需求：如果该对象需要在许多地方共享怎么办？或者如果视图 A 需要将其传递给视图 B，而视图 B 又需要将其传递给视图 C，视图 C 又需要将其传递给视图 D 呢？不难看出，这样的代码编写会非常繁琐。

SwiftUI 有一个更好的解决方案：将对象放入环境，然后用 `@Environment` 属性包装器将其读出。

这需要对代码做两个小改动。

1. 不再直接向 `HighScoreView` 传递值，而是使用 `environment()` 修改器将对象放入环境中：

```swift
VStack {
    Text("Welcome!")
    HighScoreView()
}
.environment(player)

// 此修改器是为使用 @Observable 宏的类设计的，此处便是 player
```

2. 一旦将对象放入环境，任何子视图都可以将其读出。以 `HighScoreView` 为例，我们需要将其 `player` 属性修改为这样：

```swift
@Environment(Player.self) var player

// 给定视图层次结构的环境只能容纳一个给定类型的可观察对象
// 需要在 Preview 中用 .environment(Favorites()) 注入示例对象
```

以上解决方案在大多数情况下运行良好，但在尝试使用 `@Environment` 值作为绑定时会出现问题。

像这样的代码就会出现问题：

```swift
struct HighScoreView: View {
    @Environment(Player.self) var player

    var body: some View {
        Stepper("High score: \(player.highScore)", value: $player.highScore)
    }
}
```

如果我们使用 `@State` 制作了 `player` 实例，这将是允许的，但这并不适用于 `@Environment` 。Apple 目前对此的解决方案是直接在 body 属性中使用 `@Bindable` ：

```swift
@Bindable var player = player
```

#data 