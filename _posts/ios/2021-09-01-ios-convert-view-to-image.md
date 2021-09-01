---
layout: post
title: "[iOS] UIView를 UIImage로 변환하기"
date: 2021-09-01 00:00:00
categories: iOS
tags: iOS Swift
---

![ios]({{ site.url }}/assets/logo/ios.png)

#### UIView Extension

```swift
extension UIView {

    var asImage: UIImage {
        let renderer = UIGraphicsImageRenderer(size: self.bounds.size)
        let image = renderer.image { _ in
            self.drawHierarchy(in: self.bounds, afterScreenUpdates: true)
        }
        return image
    }
}
```
