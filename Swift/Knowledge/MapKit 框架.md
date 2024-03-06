## 显示一张地图

1. 导入框架。

```swift
import MapKit 
```

2. 在 SwiftUI 视图中放置地图。

```swift
Map()
```

## 简单的自定义选项

- 可以使用 `mapStyle()` 修改器来控制地图的外观。

可以得到卫星地图：

```swift
Map()
    .mapStyle(.imagery)
```

可以将卫星地图和街道地图结合起来：

```swift
Map()
    .mapStyle(.hybrid)
```

也可以在此基础上添加真实海拔高度：

```swift
.mapStyle(.hybrid(elevation: .realistic))
```

- 可以调整用户使用地图的方式，例如是否可以缩放或旋转位置。

可以制作一张始终以特定位置为中心的地图，但用户仍然可以旋转和缩放：

```swift
Map(interactionModes: [.rotate, .zoom])
```

也可以不指定交互模式，即地图始终是完全固定的：

```swift
Map(interactionModes: [])
```

## 高级的自定义选项

- **控制位置**

1. 自定义摄像头的位置。例如，可以创建一个属性来存储伦敦的位置，跨度指定为 1 度乘 1 度：

```swift
let position = MapCameraPosition.region(
    MKCoordinateRegion(
        center: CLLocationCoordinate2D(latitude: 51.507222, longitude: -0.1275),
        span: MKCoordinateSpan(latitudeDelta: 1, longitudeDelta: 1)
    )
)
```

2. 然后，就可以用它来确定地图的初始位置：

```swift
Map(initialPosition: position)
```

3. 该值只是**初始**位置。如果要随时间改变位置，则需**标记**为 `@State` ，然后作为绑定传入：

```swift
Map(position: $position)
```

4. 现在它已被存储为程序状态，可以通过添加按钮来改变它，从而跳转到其他位置：

```swift
    Button("Paris") {
        position = MapCameraPosition.region(
            MKCoordinateRegion(
                center: CLLocationCoordinate2D(latitude: 48.8566, longitude: 2.3522),
                span: MKCoordinateSpan(latitudeDelta: 1, longitudeDelta: 1)
            )
        )
    }
```

5. 虽然现在向地图传递了绑定，但地图移动时我们无法读取位置。需要 `onMapCameraChange()` 修改器，它可以告诉我们位置是**立即**发生变化还是**移动结束**后发生变化：

```swift
Map(position: $position)
    .onMapCameraChange(frequency: .continuous) { context in
        print(context.region)
    }
```

```swift
Map(position: $position)
    .onMapCameraChange { context in
        print(context.region)
    }
```

- **放置注释**

1. 定义一个包含位置的新数据类型（必须符合 [[可识别协议 - Identifiable]]）：

```swift
struct Location: Identifiable {
    let id = UUID()
    var name: String
    var coordinate: CLLocationCoordinate2D
}
```

2. 创建一个包含所有位置的数组：

```swift
let locations = [
    Location(name: "Buckingham Palace", coordinate: CLLocationCoordinate2D(latitude: 51.501, longitude: -0.141)),
    Location(name: "Tower of London", coordinate: CLLocationCoordinate2D(latitude: 51.508, longitude: -0.076))
]
```

3. 将它们作为注释添加到地图中。最简单的一种叫做 `Marker` ：

```swift
Map {
    ForEach(locations) { location in
        Marker(location.name, coordinate: location.coordinate)
    }
}
```

4. 如果想对 `Marker` 在地图上的显示方式进行更多控制，可以使用 `Annotation` 来代替。这样就可以提供一个完全自定义的视图来代替标准的系统标记气球：

```swift
Annotation(location.name, coordinate: location.coordinate) {
    Text(location.name)
        .font(.headline)
        .padding()
        .background(.blue)
        .foregroundStyle(.white)
        .clipShape(.capsule)
}
.annotationTitles(.hidden)
```

- **处理点击**

可以使用 `onTapGesture()` 来处理地图上的点击。这会告诉我们用户在地图上点击的位置，但它是以**屏幕坐标**来表示的。

为了获取地图上的**实际位置**，我们需要一个名为 `MapReader` 的特殊[[视图 - View]]。

将该视图包裹在地图上时，就会得到一个特殊的 `MapProxy` 对象，它可以将屏幕上的位置转换成地图上的位置，反之亦然：

```swift
MapReader { proxy in
    Map()
        .onTapGesture { position in
            if let coordinate = proxy.convert(position, from: .local) {
                print(coordinate)
            }
        }
}
```

`.local` 表示在地图的本地坐标空间中转换该位置。这意味着正在处理的点击位置是相对于地图左上角的，而不是整个屏幕或其他坐标空间。

#framework 