存储少量数据的一种常用方法称为 `UserDefaults` ，它非常适合简单的用户偏好设置。您存储在 `UserDefaults` 中的所有内容都将在应用程序启动时自动加载，如果您存储了大量数据，程序的启动速度就会减慢。至少可给您一个概念，您应该将存储量控制在 512KB 以内。

`UserDefaults` 非常适合用于存储用户最后一次启动应用的时间、最后一次阅读的新闻故事或其他被动收集的信息。

SwiftUI 通常可以将 `UserDefaults` 包装在一个名为 `@AppStorage` 的漂亮而简单的[[属性包装器]]中。这个属性包装器目前仅支持部分功能，但却非常有用。

## 存储数据

以下这行按钮闭包中的代码用于保存用户的点击次数，以便再次打开时不清零：

```swift
UserDefaults.standard.set(tapCount, forKey: "Tap")
```

仅这一行代码，你就可以看到三方面的作用：

1. 我们需要使用 `UserDefaults.standard`。这是连接到我们应用程序的 `UserDefaults` 的内置实例，但在更高级的应用程序中，您可以创建自己的实例。
2. `set()` 方法可以接受任何类型的数据，如整数、布尔值、字符串等。
3. 我们为这些数据附加了一个字符串名称，在我们的例子中就是键 "Tap"。这个 key 很重要，我们需要使用相同的 key 从 `UserDefaults` 中读取数据。

## 回读数据

与其一开始就将 `tapCount` 设置为 0，不如让它像这样从 `UserDefaults` 读回数值：

```swift
@State private var tapCount = UserDefaults.standard.integer(forKey: "Tap")
```

1. 在第一次运行的时候没有 key，于是返回默认值 0。（这会有所帮助，也会造成困扰）
2. iOS 将数据写入永久存储需要几秒的间隔。（但现在哪怕迅速关闭程序，也不会丢失内容）

## @AppStorage

它可以让我们完全不使用 `UserDefaults`，而只使用 `@AppStorage` 而不是 `@State` 属性：

```swift
struct ContentView: View {
    @AppStorage("tapCount") private var tapCount = 0

    var body: some View {
        Button("Tap count: \(tapCount)") {
            tapCount += 1
        }
    }
}
```

1. 我们通过 `@AppStorage` 属性包装器访问 `UserDefaults` 系统。`@AppStorage` 工作时与 `@State` 类似：当值发生变化时，将重新调用 `body` 属性，以便我们的用户界面反映新数据。
2. 我们附加一个任意字符串名称，即我们要存储数据的 `UserDefaults` key。
3. 如果 `UserDefaults` 中没有保存现有值，则将使用我们自己提供的默认值。

`@AppStorage` 非常适合用于存储整数和布尔值等简单设置，但当涉及复杂数据（例如自定义 Swift 类型）时，我们还是需要直接探查 `UserDefaults` 本身。

#data