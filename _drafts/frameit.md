---
title:          Automating App Store screenshots
date:           2016-09-10 13:00:00
summary:        Leveraging Fastlane with Frameit to simplify App Store preparation
categories:     code reference
---

## Steps
1. Use [SimulatorStatusMagic](https://github.com/shinydevelopment/SimulatorStatusMagic) to clean up simulator status bars
2. Create new UI test target
3. Set up project with Fastlane (link to other article?)
4. Bring in `SnapshotHelper.swift`
5. Create UI tests that navigate to each screen you want in screenshots
6. In `setUp()` method, add
```swift
let app = XCUIApplication()
setupSnapshot(app)
app.launch()
```
7. Call `snapshot("[NameOfScreenshotFile]")` to generate each screenshot, e.g. `snapshot("01Launch")`
8. Create scheme for screenshots and only include screenshot bundle in Test phase
9. Set up `Snapfile` with correct values
