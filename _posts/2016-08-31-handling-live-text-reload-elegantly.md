---
title:          Handling live text reload elegantly
date:           2016-08-31 13:00:00
summary:        Easy steps to support concurrent editing without losing cursor position or text selection in UITextView
categories:     code reference
minutes:        10
---

In my current project at my day job, we are using [Firebase](https://firebase.google.com) and [ReSwift](https://github.com/ReSwift/ReSwift). I plan to write more about this powerful combination soon. One of the major advantages is that it allows us to easily support live reloading of concurrent editing. However, I ran into a problem in long-form text editing. It was impressive to see the text update while someone else edited the same data, but if you were also trying to type, it would get extremely frustrating. With every reload, your cursor would jump to the end of the text, making it nearly impossible to keep working.

One of my favorite podcasts, [Runtime](https://spec.fm/podcasts/runtime), recently mentioned approaches to diffing text. I reached out to [Sam Soffes](https://twitter.com/soffes), who pointed me to a simple library he created for this, [diff](https://github.com/soffes/diff).

Using that library, I was ready to tackle preserving the cursor position and text selection when the underlying text changed. In the hopes that others can benefit from or improve this work, here is the code that I am using:

```swift
func updateText(with newString: String?) {
    guard let textView = textView, newString = newString,
      (diffRange, changedText) = diff(textView.text, newString) else { return }
    guard let selectedRange = textView.selectedTextRange else { textView.text = newString; return }
    textView.text = newString

    let cursorOffset = textView.offsetFromPosition(textView.beginningOfDocument, toPosition: selectedRange.start)
    let selectedEndOffset = textView.offsetFromPosition(textView.beginningOfDocument, toPosition: selectedRange.end)
    let selectedRangeLength = selectedEndOffset - cursorOffset

    if selectedEndOffset < diffRange.startIndex {
        // Change is after current cursor
        moveCursorRelativeToBeginning(with: cursorOffset, rangeLength: selectedRangeLength)
    } else if cursorOffset < diffRange.startIndex && selectedEndOffset > diffRange.endIndex {
        // Change occurs within selection
        moveCursorRelativeToBeginning(with: cursorOffset, rangeLength: selectedRangeLength + changedText.characters.count - diffRange.count)
    } else if cursorOffset >= diffRange.endIndex {
        // Change occurs completely before current cursor
        moveCursorRelativeToBeginning(with: cursorOffset + changedText.characters.count - diffRange.count, rangeLength: selectedRangeLength)
    } else if diffRange.startIndex < selectedEndOffset && diffRange.startIndex > cursorOffset {
        // Change starts in middle of selection
        moveCursorRelativeToBeginning(with: cursorOffset, rangeLength: selectedRangeLength - (selectedEndOffset - diffRange.startIndex))
    } else if diffRange.startIndex <= cursorOffset && cursorOffset < diffRange.endIndex {
        // Change is a removal/change over the current cursor position
        let rangeLength = selectedRangeLength - (diffRange.endIndex - cursorOffset)
        moveCursorRelativeToBeginning(with: cursorOffset - (cursorOffset - diffRange.startIndex) + changedText.characters.count, rangeLength: rangeLength > 0 ? rangeLength : 0)
    }
}

private func moveCursorRelativeToBeginning(with offset: Int, rangeLength: Int = 0) {
    guard let textView = textView, startPosition = textView.positionFromPosition(textView.beginningOfDocument, offset: offset), endPosition = textView.positionFromPosition(startPosition, offset: rangeLength) else { return }
    textView.selectedTextRange = textView.textRangeFromPosition(startPosition, toPosition: endPosition)
}
```

This is even more useful when combined with the automated tests that ensure that it is working properly. Here is a gist with all of the tests:

{% gist benjaminsnorris/710d22ef066ae249156f7f959be7debe TextEditingSpec.swift %}
