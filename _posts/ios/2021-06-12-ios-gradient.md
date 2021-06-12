---
layout: post
title:  "[iOS] Gradient 배경 적용하기"
date:   2021-06-12 00:00:00
categories: iOS
tags: iOS Swift
---

![ios]({{ site.url }}/assets/logo/ios.png)


#### UIView Extension

```swift
extension UIView {

    func setGradientColor(colors: [UIColor], axis: NSLayoutConstraint.Axis = .vertical) {
        let gradientLayer = CAGradientLayer()
        gradientLayer.frame = self.bounds
        gradientLayer.colors = colors.map(\.cgColor)

        if axis == .horizontal {
            gradientLayer.startPoint = CGPoint(x: 0, y: 0)
            gradientLayer.endPoint = CGPoint(x: 1, y: 0)
        }

        self.backgroundColor = .clear
        self.layer.insertSublayer(gradientLayer, at: 0)
    }
}
```