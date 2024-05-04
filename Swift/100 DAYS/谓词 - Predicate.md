`@Query` 不仅可以用于按特定顺序对 [[SwiftData 框架]] 对象进行[[排序描述 - SortDescriptor|排序]]，还可用于使用谓词（**一系列应用于数据的测试，以决定返回什么数据**）对数据进行**过滤**。

一个例子如下：

```swift
@Query(filter: #Predicate<User> { user in
    user.name.contains("R")
}, sort: \User.name) var users: [User]
```

1. 过滤器以 `#Predicate<User>` 开头，这意味着我们要编写一个谓词（一个花哨的词，表示我们要进行的测试）；
2. [[闭包 - Closure]] 会遍历该类的每个对象，需要被过滤留下的则返回 True；
3. 闭包内的条件不仅可以用**逻辑操作符**连接多个，还可以用**严格**的 if 语句。

#data 