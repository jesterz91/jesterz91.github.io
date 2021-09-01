---
layout: post
title: "[iOS] UIColor로 UIImage 얻기"
date: 2021-08-25 00:00:00
categories: iOS
tags: iOS Swift
---

![ios]({{ site.url }}/assets/logo/ios.png)

#### UIColor Extension

```swift
extension UIColor {

    var asImage: UIImage {
        let rect = CGRect(x: 0, y: 0, width: 1, height: 1)
        let renderer = UIGraphicsImageRenderer(size: rect.size)
        let image = renderer.image { ctx in
            self.setFill()
            ctx.fill(rect)
        }
        return image
    }
}

```
