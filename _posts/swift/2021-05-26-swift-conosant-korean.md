---
layout: post
title:  "[Swift] 한글 초성, 중성, 종성 얻기"
date:   2021-05-26 00:00:00
categories: Swift
tags: Swift
---

![ios]({{ site.url }}/assets/logo/swift.png)


첫글자 기준으로 초성, 중성, 종성을 얻는 함수입니다.

#### 초성

```swift
func getInitialConsonant(text: String) -> String? {
    guard let firstChar = text.unicodeScalars.first?.value, 0xAC00...0xD7A3 ~= firstChar else { return nil }

    let value = ((firstChar - 0xAC00) / 28 ) / 21

    return String(format:"%C", value + 0x1100)
}
```

#### 중성
```swift
func getMiddleConsonant(text: String) -> String? {
    guard let firstChar = text.unicodeScalars.first?.value, 0xAC00...0xD7A3 ~= firstChar else { return nil }

    let value = ((firstChar - 0xAC00) / 28) % 21

    return String(format:"%C", value + 0x1161)
}
```

#### 종성
```swift
func getFinalConsonant(text: String) -> String? {
    guard let firstChar = text.unicodeScalars.first?.value, 0xAC00...0xD7A3 ~= firstChar else { return nil }

    let value = (firstChar - 0xAC00) % 28

    guard value > 0 else { return nil }

    return String(format:"%C", value + 0x11a6 + 1)
}
```