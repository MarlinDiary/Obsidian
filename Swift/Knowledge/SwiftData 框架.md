SwiftData 是一个功能强大的现代框架，用于存储、查询和过滤数据。

## 基础知识

SwiftData 就是让我们定义对象和这些对象的属性，再让我们从永久存储中读写它们的一个框架。

从表面上看，这就像使用 [[归档数据 - Codable]] 和 [[用户偏好数据 - UserDefaults]] 一样，但它要比这先进得多：SwiftData 可以对我们的数据进行排序和过滤，并且可以处理更大的数据。更棒的是，SwiftData 实现了各种更高级的功能：iCloud 同步、Lazy Loading 数据、撤消和重做等等。

## 手动定义 SwiftData Model

1. 定义要在应用程序中使用的数据：

```swift
@Observable
class Student {
    var id: UUID
    var name: String

    init(id: UUID, name: String) {
        self.id = id
        self.name = name
    }
}
```

2. 在定义上方 import 框架：

```swift
import SwiftData
```

3. 修改 [[属性包装器]]：

```swift
@Model
class Student {
```

这样的一个类称为一个 SwiftData Model，它定义了我们希望在应用程序中使用的某种数据。在幕后， `@Model` 构建在与 `@Observable` 相同的观察系统之上。

## 创建 Model Container

这段代码将告诉 SwiftData 在 iPhone 上为我们准备一些存储空间，它将在其中读写 Model 实例。

这项工作最好在 [[App Struct]] 中完成。

1. 我们需要在 `import SwiftUI` 旁边添加 `import SwiftData` ：

```swift
import SwiftData
```

2. 在 `WindowGroup` 中添加一个修饰符，这样 SwiftData 就可以在应用程序中的任何地方使用：

```swift
.modelContainer(for: Student.self)    
```

_model container_ 是 SwiftData 用来存储数据的地方。首次运行应用程序时，这意味着 SwiftData 必须创建底层数据库文件，但在以后的运行中，它将加载之前创建的数据库。

## 了解 Model Context

Model Context 实际上是数据的 "实时 "版本，当您加载对象并更改它们时，这些更改只存在于内存中，直到它们被保存。

Model Context 的作用就是让我们在内存中处理所有数据，这比不断读写数据到磁盘要快得多。

每个 SwiftData 应用程序都需要一个模型上下文来使用，而我们已经创建了我们的 Context -- 它是在我们使用 `modelContainer()` 修饰符时自动创建的。SwiftData 会自动为我们创建一个模型上下文，称为 main context，并将其存储在 SwiftUI 的环境中。

## 读取数据

从 SwiftData 中检索信息是通过查询（Query）完成的--我们描述我们想要什么、如何排序以及是否需要使用任何过滤器，然后 SwiftData 会发回所有匹配的数据。我们需要确保该查询随着时间的推移保持更新，这样当条目创建或删除时，我们的用户界面也能保持同步。

SwiftUI 对此提供了一种解决方案，另一种[[属性包装器]]。这次它被称为 `@Query` ，只要在文件中添加 `import SwiftData` 即可使用。

```swift
@Query var students: [Student]
```

这看起来像一个普通的 `Student` [[数组 - Array]]，但只要在开头添加 `@Query` 就足以让 SwiftData 从其 Model Container 中加载学生。

## 写入数据

1. 首先，我们需要一个新属性来访问之前自动创建的 Model Context：

```swift
@Environment(\.modelContext) var modelContext
```

2. 创建实例：

```swift
let student = Student(id: UUID(), name: "\(chosenFirstName) \(chosenLastName)")
```

3. 写入 modelContext：

```swift
modelContext.insert(student)
```

## 编辑数据

编辑 SwiftData 对象与编辑普通的 `@Observable` [[类 - Class]] 没有什么不同，也需要配合 [[@Bindable]] 使用，只是我们的所有数据都会被加载和保存。

1. 编辑的时候记得要 import SwiftData；
2. 编辑的时候不需要 @Environment(\.modelContext) var modelContext *（但删除需要）*。

## 按类型清空

```swift
try? modelContext.delete(model: User.self)
```

## 存储大型数据

在模型中存储图片或影片等大型数据时，请使用像这样的特殊 `@Attribute` 宏来定义它们：

```swift
@Attribute(.externalStorage) var photo: Data
```

这样，SwiftData 就不会直接在数据库中保存图像数据，而是将其放在旁边，这样性能更好。

#data #framework