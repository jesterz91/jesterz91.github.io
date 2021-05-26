---
layout: post
title:  "[iOS] 최상단 뷰 컨트롤러 얻기"
date:   2021-05-26 00:00:00
categories: iOS
tags: iOS Swift
---

![ios]({{ site.url }}/assets/logo/ios.png)


#### UIApplication extension 정의

```swift
extension UIApplication {

    func topViewController() -> UIViewController? {
        UIApplication.shared.windows
            .filter { $0.isKeyWindow }
            .first?.rootViewController?
            .topViewController()
    }
}
```
#### UIViewController extension 정의

```swift
extension UIViewController {

    func topViewController() -> UIViewController? {

        if let presented = self.presentedViewController {
            return presented.topViewController()
        }

        if let navigation = self as? UINavigationController {
            return navigation.visibleViewController?.topViewController()
        }

        if let tab = self as? UITabBarController {
            return tab.selectedViewController?.topViewController() ?? tab
        }

        return self
    }
}
```

*** 


#### 최상단 뷰컨트롤러 얻기
```swift
class SomeClass {
    
    func doSomething() {
        guard let topVC = UIApplication.shared.topViewController() else { return }

        topVC.view.backgroundColor = .blue
    }
}
```