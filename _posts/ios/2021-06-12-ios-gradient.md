---
layout: post
title:  "[iOS] Gradient 배경 적용하기"
date:   2021-06-12 00:00:00
categories: iOS
tags: iOS Swift
---

![ios]({{ site.url }}/assets/logo/ios.png)


#### Gradient 배경 색상 지정

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

#### 동일 간격으로 배경 색상 지정

```swift
extension UIView {

    func setEqualSpacingColor(colors: [UIColor], axis: NSLayoutConstraint.Axis = .vertical) {
        let gradientLayer = CAGradientLayer()
        gradientLayer.frame = self.bounds

        var cgcolors = [CGColor]()
        var locations = [NSNumber]()

        for (index, color) in colors.enumerated() {
            cgcolors += [color.cgColor, color.cgColor]
            locations += [
                NSNumber(value: (1.0 / Double(colors.count)) * Double(index)),
                NSNumber(value: (1.0 / Double(colors.count)) * Double(index + 1))
            ]
        }

        if axis == .horizontal {
            gradientLayer.startPoint = CGPoint(x: 0, y: 0)
            gradientLayer.endPoint = CGPoint(x: 1, y: 0)
        }
      
        gradientLayer.colors = cgcolors
        gradientLayer.locations = locations

        self.backgroundColor = .clear
        self.layer.insertSublayer(gradientLayer, at: 0)
    }
}
```