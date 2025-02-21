## 结构由 Property 和 Method 组成

```swift
struct Album {
    let title: String
    let artist: String
    let year: Int

    func printSummary() {
        print("\(title) (\(year)) by \(artist)")
    }
}

// 如果 func 修改了 prop，就需要在 func 前加上 mutating
```

## 计算属性 - Computed Property

```swift
    var vacationRemaining: Int {
        vacationAllocated - vacationTaken
    }

// 计算属性的访问方式类似于存储属性，但工作方式类似于函数
```

## 计算属性的 Getter 和 Setter

```swift
var vacationRemaining: Int {
    get {
        vacationAllocated - vacationTaken
    }

    set {
        vacationAllocated = vacationTaken + newValue
    }
}

// get 可以被理解为 Read，set 可以被理解为 Write
```

## 计算属性的 Did Set 和 Will Set

```swift
struct App {
    var contacts = [String]() {
        willSet {
            print("Current value is: \(contacts)")
            print("New value will be: \(newValue)")
        }

        didSet {
            print("There are now \(contacts.count) contacts.")
            print("Old value was \(oldValue)")
        }
    }
}

// property observers
```

## 访问控制

在变量前加 `private` `private(set)`  `public` 等符号

## 静态属性

### 静态属性的创建

```swift
struct School {
    static var studentCount = 0

    static func add(student: String) {
        print("\(student) joined the school.")
        studentCount += 1
    }
}
```

### 静态属性的调用

```swift
School.add(student: "Taylor Swift")
print(School.studentCount)
```

## 其他

- 结构用于创建自己的数据类型
- 我们用大写字母开始所有数据类型（ `Int` , `Double` , `Bool` 等）
- 结构体的成员（属性和方法）不存在声明顺序的限制，这意味着你可以在结构体内部的任何位置声明方法，并且这些方法都可以互相调用，无论它们在代码中的具体位置如何

#struct #hard 