---
layout: post
title:  "[Android] View 중복클릭 방지하기"
date:   2021-04-14 00:00:00
categories: Android
tags: Android Kotlin RxJava RxBinding
---

![android]({{ site.url }}/assets/logo/android.png)

뷰를 연속으로 클릭하여 발생하는 중복클릭 현상을 방지하기 위해서는 `View.OnClickListener` 를 확장하여 사용하거나,
`RxJava`, `RxBinding` 의 오퍼레이터를 활용하는 방법이 있습니다.

***
### 1. View.OnClickListener 확장

#### OnSafeClickListener 정의

```kotlin
class OnSafeClickListener(private val onSafeClick: (View) -> Unit) : View.OnClickListener {

    override fun onClick(view: View?) {
        view ?: return

        if (view.isClickable) {
            onSafeClick(view)

            view.isClickable = false

            // 0.5초간 중복클릭 방지
            view.postDelayed(500L) {
                view.isClickable = true
            }
        }
    }
}
```


#### 확장함수 정의

```kotlin
fun View.setOnSafeClickListener(onClick: (View) -> Unit) {
    setOnSafeClickListener(View.OnClickListener(onClick))
}

fun View.setOnSafeClickListener(listener: View.OnClickListener) {
    setOnClickListener(OnSafeClickListener(listener::onClick))
}
```


#### 확장함수 사용
```kotlin
class MainActivity : AppCompatActivity() {
    ...
    override fun onCreate(savedInstanceState: Bundle?) {
        ...
        view.setOnSafeClickListener { view ->
            // TODO 
        }
    }
}
```

```kotlin
class MainActivity : AppCompatActivity(), View.OnClickListener {
    ...
    override fun onCreate(savedInstanceState: Bundle?) {
        ...
        view1.setOnSafeClickListener(this)
        view2.setOnSafeClickListener(this)
    }

    override fun onClick(v: View?) {
        when (v) {
            view1 -> {/* TODO */}
            view2 -> {/* TODO */}
        }
    }
}
```
***
### 2. RxBinding 활용

[![Xcode]({{ site.url }}/assets/reactivex/throttle_first.png)]({{ site.url }}/assets/reactivex/throttle_first.png){: data-lightbox="imgs" }

`RxJava`와 `RxBinding`을 사용하고 있는 경우, 
`clicks`, `throttleFirst` 오퍼레이터를 사용하여 중복클릭을 방지할 수 있습니다.

#### 확장함수 정의

```kotlin
fun View.safeClicks(): Observable<Unit> {
    return clicks().throttleFirst(500L, TimeUnit.MILLISECONDS) // 0.5초간 중복클릭 방지
                   .observeOn(AndroidSchedulers.mainThread())
}
```

#### 확장함수 사용

```kotlin
class MainActivity : AppCompatActivity() {
    ...
    override fun onCreate(savedInstanceState: Bundle?) {
        ...
        view.safeClicks()
            .subscribe {/* TODO */}
            .addTo(compositeDisposable)
    }
}
```

