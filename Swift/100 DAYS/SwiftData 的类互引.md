[[SwiftData 框架]] 允许我们创建相互引用的模型，例如，一个 `School` 模型拥有一个由多个 `Student` 对象组成的数组，或者一个 `Employee` 模型存储一个 `Manager` 对象。

## 相互引用的创建

只要你告诉 SwiftData 你想要什么，它就能很好地自动形成这些相互引用关系。

比如，如果有以下 User 模型：

```swift
@Model
class User {
    var name: String
    var city: String
    var joinDate: Date
    
    var jobs = [Job]()

    init(name: String, city: String, joinDate: Date) {
        self.name = name
        self.city = city
        self.joinDate = joinDate
    }
}
```

如果我们还有一个 Job 模型：

```swift
@Model
class Job {
    var name: String
    var priority: Int
    var owner: User?

    init(name: String, priority: Int, owner: User? = nil) {
        self.name = name
        self.priority = priority
        self.owner = owner
    }
}
```

在属性的相互引用中，双向关系就创建完成了。

## modelContainer 的省略

当我们在 `App` 结构中使用 `modelContainer()` 修饰符时，我们传递了 `User.self` 以便 SwiftData 知道要为该模型设置存储。我们不需要在此处添加 `Job.self` ，因为 SwiftData 可以看到两者之间存在关系，因此它会自动处理这两个关系。

## 细节问题

我们已经将 `User` 和 `Job` 链接起来，这样一个用户就可以有很多 Jobs 要做，但是如果我们删除了一个 User，会发生什么情况呢？

答案是所有的 Jobs 都会保持不变，不会被删除。

## @Relationship

如果您特别希望同时删除 User 的所有 Jobs 对象，我们需要告诉 SwiftData 这一点。为此，我们需要使用 `@Relationship` 宏，并为其提供删除规则。

默认的删除规则称为 `.nullify` ，这意味着每个 `Job` 对象的 `owner` 属性都会被设置为 nil，表示它们没有所有者。我们将把它改为 `.cascade` ，这意味着删除一个 `User` 将自动删除它们的所有 `Job` 对象。

之所以称其为级联（_cascade_），是因为删除会持续到所有相关对象--例如，如果我们的 `Job` 对象有 `locations` 关系，那么这些对象也会被删除，依此类推。

```swift
@Relationship(deleteRule: .cascade) var jobs = [Job]()
```

#class #data #hard 