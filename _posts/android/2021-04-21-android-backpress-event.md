---
layout: post
title:  "[Android] BackPress 이벤트 처리하기"
date:   2021-04-21 00:00:00
categories: Android
tags: Android Kotlin RxJava
---

![android]({{ site.url }}/assets/logo/android.png)

사용자가 백 버튼을 누를 경우 앱이 바로 종료되면 불편함을 느낄 수 있습니다.
이 경우 BackPress 이벤트가 발생되는 시간차를 이용하여 앱을 종료하는 처리를 할 수 있습니다.

***

```kotlin
class MainActivity : AppCompatActivity() {
    ...
    private val backPressSubject = BehaviorSubject.createDefault(0L)

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        backPressSubject.buffer(2, 1)
                .map { it[1] - it[0] }
                .subscribe(::handleBackPressEvent)
                .addTo(disposables)
    }

    override fun onBackPressed() = backPressSubject.onNext(System.currentTimeMillis())

    private fun handleBackPressEvent(interval: Long) {
        // interval이 2초 미만이면 앱 종료
        if (interval < 2000) {
            super.onBackPressed()
        } else {
            Toast.makeText(this, "앱을 종료 하려면 한번 더 눌러주세요.", Toast.LENGTH_SHORT).show()
        }
    }
    ...
}
```
참고

- [뱅크샐러드 기술블로그][link]

[link]: https://medium.com/banksalad/handling-back-button-with-rxjava-d948d8d3db80
