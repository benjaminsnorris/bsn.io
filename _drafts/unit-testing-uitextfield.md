---
title:          Unit testing UITextField and UITextView
date:           
summary:        The challenges of writing tests
categories:     code reference testing
---

```swift
  let textField = UITextField()

  let initialPosition = textField.beginningOfDocument // `nil` when not `firstResponder`
  let success = textField.becomeFirstResponder() // `false` when no `UIWindow` in view ancestry
```
