## 动态筛选

最好的办法是使用**初始化器**向视图传递一个值，然后使用该值创建查询。

```swift
init(minimumJoinDate: Date) {
    _users = Query(filter: #Predicate<User> { user in
        user.joinDate >= minimumJoinDate
    }, sort: \User.name)
}
```

在 `users` 之前有一个下划线，这是有意为之：我们并不是要更改 `User` 数组，而是要更改产生该数组的 [[谓词 - Predicate|SwiftData 查询]]。下划线是 Swift 访问该查询的方式。

## 动态排序

```swift
init(minimumJoinDate: Date, sortOrder: [SortDescriptor<User>]) {
    _users = Query(filter: #Predicate<User> { user in
        user.joinDate >= minimumJoinDate
    }, sort: sortOrder)
}
```

[[排序描述 - SortDescriptor]] 类型需要知道它要排序什么，因此需要在角括号内指定 Class/Type 。

#data 