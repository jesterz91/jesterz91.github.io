---
layout: post
title:  "[iOS] 버튼의 배경색을 state 별로 지정하기"
date:   2021-04-13 00:00:00
categories: iOS
tags: iOS Swift
---

![ios]({{ site.url }}/assets/logo/ios.png)

버튼의 배경색을 State 별로 지정하고 싶은 경우 extension을 정의하여 사용할 수 있습니다.

***

#### 버튼 extension 정의

```swift
extension UIButton {

    func setBackgroundColor(_ color: UIColor, for state: UIControl.State) {
        UIGraphicsBeginImageContext(CGSize(width: 1.0, height: 1.0))

        guard let context = UIGraphicsGetCurrentContext() else { return }
        context.setFillColor(color.cgColor)
        context.fill(CGRect(x: 0.0, y: 0.0, width: 1.0, height: 1.0))

        let backgroundImage = UIGraphicsGetImageFromCurrentImageContext()
        UIGraphicsEndImageContext()

        self.setBackgroundImage(backgroundImage, for: state)
    }
}
```

***

#### 버튼 extension 사용

```swift
button.setBackgroundColor(.systemRed, for: .normal)
button.setBackgroundColor(.systemBlue, for: .disabled)
```

***

출처

- [무과장의 개발로 개발][link]

[link]: https://jmkim0213.github.io/ios/swift/ui/2019/02/05/button_background.html