MVVM 是 Model View View-Model 的缩写，可以将之理解为一种将**逻辑**与**布局**分离开来的方法，也可以理解为一种将**管理数据**与**展示数据**分离开来的方法。

## 分离状态片段

1. 新建名为 ContentView-ViewModel 的 Swift 文件。我们将用它创建一个新类来管理数据，并代表 `ContentView` 结构操作数据，这样视图就不会真正关心底层数据系统是如何工作的了。

2. 创建一个使用 `Observable` 宏的新类。这样就能向任何正在观察的 SwiftUI 视图报告更改：

```swift
@Observable
class ViewModel {
}
```

3. 将新类放在 `ContentView` 的[[扩展 - Extension]]中。这样就避免了对类名的污染：

```swift
extension ContentView {
    @Observable
    class ViewModel {
    }
}
```

4. 现在类已经就位，可选择将视图中的哪些**状态片段**移动到视图模型中。比如，将 `ContentView` 中的 `@State` 属性移到其 view model 中，移除 `@State private` 部分，因为它们不再需要：

```swift
extension ContentView {
    @Observable
    class ViewModel {
        var locations = [Location]()
        var selectedPlace: Location?
    }
}
```

5. 现在，我们可以用一个属性替换 `ContentView` 中的所有属性：

```swift
@State private var viewModel = ViewModel()
```

6. 这会破坏很多代码，但修复起来很简单，只需在不同位置添加 `viewModel` 即可。

## 分离数据操作

View 在处理**数据展示**时效果最佳，这意味着**数据操作**是移入 View Model 的最佳选择。

1. 将 View Model 中的属性修改为以下内容。这样就避免了外部的数据写入：

```swift
private(set) var locations = [Location]()
```

2. 通过在类中添加方法的方式，将需要写入数据的部分移入 View Model：

```swift
func addLocation(at point: CLLocationCoordinate2D) {
    let newLocation = Location(id: UUID(), name: "New location", description: "", latitude: point.latitude, longitude: point.longitude)
    locations.append(newLocation)
}
```

#swiftui 