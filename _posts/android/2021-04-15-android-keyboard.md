---
layout: post
title:  "[Android] 키보드 보이기/숨기기"
date:   2021-04-15 00:00:00
categories: Android
tags: Android Kotlin
---

![android]({{ site.url }}/assets/logo/android.png)

프로그래밍 방식으로 키보드를 노출하거나 감추고싶을경우 확장함수를 정의하여 사용할 수 있습니다.

***

#### View 확장함수 정의

```kotlin
fun View.showKeyboard(): Boolean {
    val imm = context.getSystemService<InputMethodManager>()
    return imm?.showSoftInput(this, 0) ?: false
}

fun View.hideKeyboard(): Boolean {
    val imm = context.getSystemService<InputMethodManager>()
    return imm?.hideSoftInputFromWindow(windowToken, 0) ?: false
}
```

#### View 확장함수 사용
```kotlin
view.showKeyboard() // 키보드 보이기

view.hideKeyboard() // 키보드 숨기기
```