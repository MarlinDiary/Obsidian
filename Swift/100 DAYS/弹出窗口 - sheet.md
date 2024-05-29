SwiftUI 中有多种显示[[视图 - View]]的方法，其中最基本的一种是 sheet：在现有视图的基础上显示新视图。

sheet 的工作原理与[[警报 - Alert]]非常相似，因为我们不会直接使用 `mySheet.present()` 或类似代码来显示 sheet。相反，我们定义了应显示 sheet 的条件，当这些条件变为 true 或 false 时，sheet 将分别显示或取消。

## 显示新视图的四个步骤

1. 我们需要一些状态来跟踪 sheet 是否显示：

```swift
@State private var showingSheet = false
```

2. 我们需要在点击按钮时切换布尔值：

```swift
showingSheet.toggle()
```

3. 我们需要将 sheet 附加到视图的某处（`sheet()` 和 `alert()` 一样是一个修饰符）：

```swift
.sheet(isPresented: $showingSheet) {
    // contents of the sheet
}
```

4. 我们需要决定工作表中应该包含哪些内容：

```swift
.sheet(isPresented: $showingSheet) {
            SecondView()
        }
```

当您创建这样一个 SecondView() 视图时，您可以传入它工作所需的任何参数：

```swift
struct SecondView: View {
    let name: String

    var body: some View {
        Text("Hello, \(name)!")
    }
}
```

## 让视图因按下按钮而消失

要取消另一个视图，我们需要另一个[[属性包装器]] `@Environment` ，它允许我们创建一种属性，这种属性用于存储外部提供给我们的值。

将此属性添加到 `SecondView` 中，它会根据环境中的值创建一个名为 `dismiss` 的属性：

```swift
@Environment(\.dismiss) var dismiss
```

然后就可以添加一个用于 dismiss 该视图的按钮：

```swift
Button("Dismiss") {
    dismiss()
}
```

## 显示新视图的另一种方法

1. 添加一个新的属性：

```swift
@State private var selectedPlace: Location?
```

只要我们在[[可选项 - Optional]]中输入一个值，就等于告诉 SwiftUI 显示工作表，而当工作表被取消时，该值将自动设置回 `nil` 。

2. 附加修改器：

```swift
.sheet(item: $selectedPlace) { place in
    Text(place.name)
}
```

## 关闭时调用函数

可以为 sheet 附加一个函数，当 sheet 被取消时，该函数将自动运行。

```swift
.sheet(isPresented: $showingEditScreen, onDismiss: resetCards)
```

## 无参数视图的简易传递

与其创建一个调用初始化器的闭包，不如直接将视图传递给 sheet：

```swift
.sheet(isPresented: $showingEditScreen, onDismiss: resetCards, content: EditCards.init)
```

这种方法使用的前提是视图的初始化器不接受任何参数，否则仍需要使用基于闭包的方法。

## 显示制动器

显示制动器可以使 sheet 占用的空间小于全屏空间。这可以使用 `presentationDetents()` 修饰符来实现，该修饰符可接受用于 sheet 的一组尺寸。

例如，可以这样指定中号和大号：

```swift
Text(selectedUser.id)
    .presentationDetents([.medium, .large])
```

sheet 首次显示时将使用初始尺寸，但 iOS 会显示一个小把手，让用户将 sheet 拉到全尺寸。

#swiftui #easy 