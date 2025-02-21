## Break 和 Continue 的区别

当您想跳过当前循环迭代的剩余部分时，请使用 `continue` ；当您想跳过所有剩余的循环迭代时，请使用 `break` 。

## 用 Continue 跳过 Loop

```swift
let filenames = ["me.jpg", "work.txt", "sophie.jpg", "logo.psd"]

for filename in filenames {
    if filename.hasSuffix(".jpg") == false {
        continue
    }

    print("Found picture: \(filename)")
}
```

## 用 Break 跳过 Loop

```swift
let number1 = 4
let number2 = 14
var multiples = [Int]()

for i in 1...100_000 {
    if i.isMultiple(of: number1) && i.isMultiple(of: number2) {
        multiples.append(i)

        if multiples.count == 10 {
            break
        }
    }
}

print(multiples)
```

#loop #easy 