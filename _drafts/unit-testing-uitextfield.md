---
title:          Unit testing UITextField and UITextView
date:           2016-09-23 09:00:00
summary:        The challenges of writing tests
categories:     code reference testing
---

```swift
  let textField = UITextField()

  let initialPosition = textField.beginningOfDocument // `nil` when not `firstResponder`
  let success = textField.becomeFirstResponder() // `false` when no `UIWindow` in view ancestry
```
