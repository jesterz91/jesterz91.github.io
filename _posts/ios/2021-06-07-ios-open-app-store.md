---
layout: post
title:  "[iOS] 앱 스토어 열기"
date:   2021-06-07 00:00:00
categories: iOS
tags: iOS Swift
---

![ios]({{ site.url }}/assets/logo/ios.png)


#### App Store로 이동

```swift
let appStoreAppID = "1111111111"

guard let url = URL(string: "itms-apps://itunes.apple.com/app/id\(appStoreAppID)") else { return }

if UIApplication.shared.canOpenURL(url) {
    UIApplication.shared.open(url, options: [:], completionHandler: nil)
}
```