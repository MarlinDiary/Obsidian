## 闭包表达式

闭包可以被用于 [[结构 - Struct]] [[类 - Class]] [[枚举 - Enum]] 的属性，也可以被用于函数。

### 示范 ①

```swift
let sayHello = {
    print("Hi there!")
}

sayHello()

// 实际上是一个不带参数、不返回值的函数
```

### 示范 ②

```swift
let sayHello = { (name: String) -> String in
    "Hi \(name)!"
}

sayHello("Taylor")

// 外部参数名只有在我们直接调用函数时才重要，而不是在我们创建闭包时
```

## 闭包中的重要推演

### 创建函数并调用

```swift
let captainFirstTeam = team.sorted(by: captainFirstSorted)
```

### 使用闭包

```swift
let captainFirstTeam = team.sorted(by: { (name1: String, name2: String) -> Bool in
    if name1 == "Suzanne" {
        return true
    } else if name2 == "Suzanne" {
        return false
    }

    return name1 < name2
})
```

### 使用尾部闭包语法

```swift
let captainFirstTeam = team.sorted { name1, name2 in
    if name1 == "Suzanne" {
        return true
    } else if name2 == "Suzanne" {
        return false
    }

    return name1 < name2
}
```

闭包中的参数顺序与书写顺序是一致的。在 Swift 中，当你定义一个闭包，参数的顺序是根据你在闭包中列出的顺序来决定的。所以，上文的 name1 必然是 $0。

### 使用速记语法

```swift
let captainFirstTeam = team.sorted {
    if $0 == "Suzanne" {
        return true
    } else if $1 == "Suzanne" {
        return false
    }

    return $0 < $1
}
```

## 接受多个闭包的情况

```swift
doImportantWork {
    print("This is the first work")
} secondName: {
    print("This is the second work")
} thirdName: {
    print("This is the third work")
}
```

#closure