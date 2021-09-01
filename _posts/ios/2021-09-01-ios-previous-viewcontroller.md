---
layout: post
title: "[iOS] 이전 뷰 컨트롤러 얻기"
date: 2021-08-25 00:00:00
categories: iOS
tags: iOS Swift
---

![ios]({{ site.url }}/assets/logo/ios.png)

#### UIViewController Extension

```swift
extension UIViewController {

    var previousViewController: UIViewController? {
        if let controllersOnNavStack = self.navigationController?.viewControllers {

            let count = controllersOnNavStack.count

            // if self is still on Navigation stack
            if controllersOnNavStack.last === self, count > 1 {
                return controllersOnNavStack[count - 2]
            } else if count > 0 {
                return controllersOnNavStack[count - 1]
            }
        }
        return nil
    }
}
```
