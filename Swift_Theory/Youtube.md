# YouTube
유튭에서 공식 지원하는 라이브러리
https://github.com/youtube/youtube-ios-player-helper 
쓰면 되는데,

기능이 제법 많이 제한적임..

[ 전체화면 돌입, 탈출 디텍팅 방법 ]
~~~
override func viewDidLoad() {
    super.viewDidLoad()
    
    ...
    
    NotificationCenter.default.addObserver(self, selector: #selector(didExitFullScreen), name: UIWindow.didBecomeHiddenNotification , object: nil)
    NotificationCenter.default.addObserver(self, selector: #selector(didEnterFullScreen), name: UIWindow.didBecomeVisibleNotification , object: nil)
}
@objc func didEnterFullScreen() {
    print("전체화면 돌입")
}

@objc func didExitFullScreen() {
    print("전체화면 탈출")
}
~~~
