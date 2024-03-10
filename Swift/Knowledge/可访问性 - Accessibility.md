## 修饰符

| 修饰符                              | 作用                                            |
| -------------------------------- | --------------------------------------------- |
| .accessibilityLabel()            | 会被立即读取，应该是一段简短的文字，如“Delete”                   |
| .accessibilityHint()             | 会在短暂延迟后读取，如“Deletes an email from your inbox” |
| .accessibilityAddTraits()        | 可以描述视图是如何工作的，如 .isButton                      |
| .accessibilityRemoveTraits()     | 可以删去某些特征                                      |
| Image(decorative:)               | 让 VoiceOver 忽略该图片，除非有 Traits                  |
| .accessibilityHidden()           | 让 VoiceOver 完全忽略该视图                           |
| .accessibilityElement(children:) | 用于父视图，可以 combine 子视图，也可以 ignore 子视图           |
| .accessibilityValue()            | 将控件的 Value 与 Label 分开                         |
| .accessibilityAdjustableAction() | 自定义 increment 和 decrement 轻扫操作                |
| .accessibilityInputLabels()      | 接受一个字符串数组，这样就能通过语音多方式触发按钮                     |

#swiftui 