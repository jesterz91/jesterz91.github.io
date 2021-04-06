---
layout: post
title:  "[iOS] 프로젝트 설정 (스토리보드 제거)"
date:   2021-04-05 00:00:00
categories: iOS
tags: iOS Swift
---

![ios]({{ site.url }}/assets/logo/ios.png)


iOS 프로젝트 생성 시 User Interface를 Storyboard로 설정한 경우 스토리보드를 제거하고 싶은 경우가 있습니다.
스토리보드를 제거하려면 다음과 같은 방법을 사용할 수 있습니다.

<!-- #### Xcode 설정 -->
#### 1. Main.storyboard 파일 삭제

[![Xcode]({{ site.url }}/assets/post/ios/20210405/xcode0.png)]({{ site.url }}/assets/post/ios/20210405/xcode0.png){: data-lightbox="imgs" }

***
#### 2. 프로젝트 General > Deployment Info
[![Xcode]({{ site.url }}/assets/post/ios/20210405/xcode1.png)]({{ site.url }}/assets/post/ios/20210405/xcode1.png){: data-lightbox="imgs" }

Main Interface 영역에 Main을 지우고 빈칸으로 변경

***

#### 3. Info.plist
[![Xcode]({{ site.url }}/assets/post/ios/20210405/xcode2.png)]({{ site.url }}/assets/post/ios/20210405/xcode2.png){: data-lightbox="imgs" }

Info.plist에서 Storyboard Name 제거

***

#### 4. SceneDelegate
{% highlight swift %}
import UIKit

class SceneDelegate: UIResponder, UIWindowSceneDelegate {

    var window: UIWindow?

    func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        guard let windowScene = (scene as? UIWindowScene) else { return }
        window = UIWindow(frame: UIScreen.main.bounds)
        window?.windowScene = windowScene
        window?.rootViewController = UINavigationController(rootViewController: ViewController())
        window?.makeKeyAndVisible()
    }
}

{% endhighlight %}