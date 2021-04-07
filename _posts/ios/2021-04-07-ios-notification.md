---
layout: post
title:  "[iOS] UserNotification 프레임워크를 이용한 알림구현"
date:   2021-04-07 00:00:00
categories: iOS
tags: iOS Swift
---

![ios]({{ site.url }}/assets/logo/ios.png)

앱 내부에서 만든 메시지를 사용자에게 알리고 싶을경우 
UserNotificationCenter를 사용하여 메시지를 전달할 수 있습니다.

***

#### 1. 알림허용 요청

로컬/푸시 알림을 사용하기 위해서는 알림 설정 환경을 정의하고, 사용자에게 승인을 받아야 합니다.

{% highlight swift %}
import UIKit
import UserNotifications

@main
class AppDelegate: UIResponder, UIApplicationDelegate {

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        
        // 경고창, 배지, 사운드를 사용하는 알림 환경 정보 생성, 동의 여부창 실행
        let notificationCenter = UNUserNotificationCenter.current()
        notificationCenter.delegate = self
        notificationCenter.requestAuthorization(options: [.alert, .badge, .sound]) { (didAllow, error) in
            didAllow ? print("알림허용") : print("알림거부")
        }
        return true
    }
}
{% endhighlight %}
***

#### 2. UNUserNotificationCenterDelegate 프로토콜 채택

받은 알림을 처리하기위해 UNUserNotificationCenterDelegate 프로토콜을 채택하여
알림 처리를 위한 메서드를 구현해 줍니다.

{% highlight swift %}
extension AppDelegate: UNUserNotificationCenterDelegate {

    func userNotificationCenter(_ center: UNUserNotificationCenter, willPresent notification: UNNotification, withCompletionHandler completionHandler: @escaping (UNNotificationPresentationOptions) -> Void) {
        
        completionHandler([.list, .badge, .sound])
    }
    
    func userNotificationCenter(_ center: UNUserNotificationCenter, didReceive response: UNNotificationResponse, withCompletionHandler completionHandler: @escaping () -> Void) {
        let identifier = response.notification.request.identifier
        let userInfo = response.notification.request.content.userInfo
        
        switch identifier {
        case "id":
            print(userInfo["key"]!)
        default:
            break
        }
    }
}
{% endhighlight %}

***

#### 3. 알림 보내기

알림을 보내기 위해서는
UNUserNotificationCenter에 알림요청 객체인 UNNotificationRequest를 추가해주면 됩니다.

{% highlight swift %}
private func sendNotification(identifier: String, interval: TimeInterval) {
    UNUserNotificationCenter.current().getNotificationSettings { (settings) in
        
        guard settings.authorizationStatus == UNAuthorizationStatus.authorized else { return }
        
        DispatchQueue.main.async {

            // 알림 콘텐츠 객체
            let content = UNMutableNotificationContent()
            content.title = "알림 타이틀"
            content.body = "알림 내용"
            content.userInfo = ["key":"value"]
            content.badge = 1
            content.sound = UNNotificationSound.default
            
            // 알림 발송조건 객체
            let trigger = UNTimeIntervalNotificationTrigger(timeInterval: interval, repeats: false)
            
            // 알림 요청 객체
            let request = UNNotificationRequest(identifier: identifier, content: content, trigger: trigger)
            
            UNUserNotificationCenter.current().add(request, withCompletionHandler: nil)
        }
    }
}
{% endhighlight %}
