---
layout: post
title:  "[iOS] 앱 버전 확인"
date:   2021-06-11 00:00:00
categories: iOS
tags: iOS Swift
---

![ios]({{ site.url }}/assets/logo/ios.png)


#### App Version

```swift
guard let version = Bundle.main.infoDictionary?["CFBundleShortVersionString"] as? String else { return }
```