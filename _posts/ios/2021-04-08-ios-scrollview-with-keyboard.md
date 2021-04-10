---
layout: post
title:  "[iOS] 스크롤뷰와 키보드의 상호작용"
date:   2021-04-08 00:00:00
categories: iOS
tags: iOS Swift NotificationCenter
---

![ios]({{ site.url }}/assets/logo/ios.png)

스크롤뷰에서 텍스트필드를 사용할 경우 키보드에 의해 뷰가 가려지는 현상이 발생할수 있습니다.
키보드 이벤트 Notification에 대한 옵저버를 등록하여 뷰가 키보드에 의해 가려지는 현상을 방지할 수 있습니다. 

***

#### 1. 스크롤뷰 keyboardDismissMode 설정

스크롤뷰가 드래그 될 경우 키보드가 사라질 수 있도록 코드를 추가 합니다.

```swift
private func setKeyboardDismissMode() {
    self.scrollView.keyboardDismissMode = .onDrag
}
```

***

#### 2. Observer 등록/해제

`keyboardWillShowNotification`, `keyboardWillHideNotification` 알림을 받을수 있도록 
Observer를 등록/해제 하는 코드를 추가해 줍니다.

```swift
override func viewWillAppear(_ animated: Bool) {
    super.viewWillAppear(animated)
    
    NotificationCenter.default.addObserver(
        self,
        selector: #selector(keyboardWillShow(_:)),
        name: UIResponder.keyboardWillShowNotification,
        object: nil
    )
    
    NotificationCenter.default.addObserver(
        self,
        selector: #selector(keyboardWillHide(_:)),
        name: UIResponder.keyboardWillHideNotification,
        object: nil
    )
}

override func viewWillDisappear(_ animated: Bool) {
    super.viewWillDisappear(animated)

    NotificationCenter.default.removeObserver(self)
}
```

***

#### 3. 키보드 이벤트 Notification 처리

키보드 이벤트에 대한 알림을 받아 스크롤뷰의 contentInset 설정을 해주면,
키보드에 의해 뷰가 가려지는 현상을 방지할 수 있습니다.

```swift
@objc private func keyboardWillShow(_ notification: Notification) {
    guard let keyboardFrame = notification.userInfo?[UIResponder.keyboardFrameEndUserInfoKey] as? CGRect else { return }

    let insets = UIEdgeInsets(top: 0, left: 0, bottom: keyboardFrame.height, right: 0)
    setScrollViewContentInset(contentInset: insets)
}

@objc private func keyboardWillHide(_ notification: Notification) {

    setScrollViewContentInset(contentInset: .zero)
}

private func setScrollViewContentInset(contentInset: UIEdgeInsets) {
    self.scrollView.contentInset = contentInset
    self.scrollView.scrollIndicatorInsets = contentInset
}
```