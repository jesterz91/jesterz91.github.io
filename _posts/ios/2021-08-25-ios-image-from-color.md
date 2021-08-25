---
layout: post
title: "[iOS] UIColor로 UIImage 얻기"
date: 2021-08-25 00:00:00
categories: iOS
tags: iOS Swift
---

![ios]({{ site.url }}/assets/logo/ios.png)

#### UIImage Extension

```swift
extension UIImage {

    static func from(color: UIColor) -> UIImage {
        let rect = CGRect(x: 0, y: 0, width: 1, height: 1)
        UIGraphicsBeginImageContext(rect.size)
        let context = UIGraphicsGetCurrentContext()!
        context.setFillColor(color.cgColor)
        context.fill(rect)
        let image = UIGraphicsGetImageFromCurrentImageContext()
        UIGraphicsEndImageContext()
        return image!
    }
}
```
