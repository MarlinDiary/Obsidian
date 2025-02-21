## 字符串 → 字符串[[数组 - Array|数组]]

Swift 为我们提供了一个名为 `components(separatedBy:)` 的方法，如以**换行**为拆分点：

```swift
let input = """
            a
            b
            c
            """
let letters = input.components(separatedBy: "\n")
```

另一种方法：

```swift
Array("Hello SwiftUI")
```

## 首尾字符删减

`trimmingCharacters(in:)` 要求 Swift 删除字符串开头和结尾的某些字符。

它使用了一种名为 `CharacterSet` 的新类型，但大多数情况下，我们使用一种**内置**的特定行为：一次性删除空白和新行（指空格、制表符和换行符）。

```swift
let trimmed = letter?.trimmingCharacters(in: .whitespacesAndNewlines)
```

## 检查拼写错误的单词

该功能通过[[类 - Class|类]] `UITextChecker` 提供，名称中的 "UI "有两个附加含义：

1. 该类来自 UIKit；
2. 它是使用苹果的旧版语言 Objective-C 编写的。

检查字符串中是否有拼写错误的单词总共需要四个步骤：

1. 创建一个要检查的单词和一个 `UITextChecker` 的实例，用于检查该字符串：

```swift
let word = "swift"
let checker = UITextChecker()
```

2. 告诉 checker 我们想要检查多少字符串（由于 Objective-C 存储字符的方式相对原始，所以要以 UTF-16 编码作为桥接，并以字符串的**全长**作为范围）：

```swift
let range = NSRange(location: 0, length: word.utf16.count)
```

3. 要求 checker 报告它在我们的单词中发现了哪些拼写错误：

```swift
let misspelledRange = checker.rangeOfMisspelledWord(in: word, range: range, startingAt: 0, wrap: false, language: "en")
```

4. 检查拼写结果是否有误（因为 Objective-C 没有 [[可选项 - Optional]] 的概念，有错误的时候会返回 NSRange 的实例，没有错误的时候会返回特殊值 **NSNotFound**）：

```swift
let allGood = misspelledRange.location == NSNotFound
```

## 其他

| 修饰符 | 作用 |
| ---- | ---- |
| .remove | 移除字符串中特定位置的字符 |
| .firstIndex(of:) | 用于找到集合（例如数组、字符串等）中指定元素首次出现的位置 |

#string #type #objectivec #easy 