---
layout: post
title:  "[iOS] TextField 글자수 제한하기"
date:   2021-04-09 00:00:00
categories: iOS
tags: iOS Swift
---

![ios]({{ site.url }}/assets/logo/ios.png)

TextField를 사용할 경우, 최대 입력 글자수를 제한하고 싶은경우가 있습니다.
UITextFieldDelegate 프로토콜을 채택하여 글자수를 제한할 수 있습니다.

***

#### 1. delegate 설정

TextField에 delegate를 설정합니다.

```swift
textField.delegate = self // ViewController
```

***

#### 2. delegate 구현

UITextFieldDelegate 의 메서드를 구현하여 최대글자수 이상 입력을 막는 코드를 추가합니다.

```swift
extension ViewController: UITextFieldDelegate {

    func textField(_ textField: UITextField, shouldChangeCharactersIn range: NSRange, replacementString string: String) -> Bool {
        let maxLength = 10
        let currentText = textField.text ?? ""

        guard let strRange = Range(range, in: currentText) else { return false }

        let newText = currentText.replacingCharacters(in: strRange, with: string)

        return newText.count <= maxLength
    }
}
```