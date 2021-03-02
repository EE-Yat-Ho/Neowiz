[ 앱이 백그라운드로 가는거 감지하기 ]
if #available(iOS 13.0, *) {
    NotificationCenter.default.addObserver(self, selector: #selector(taskFunc), name: UIScene.willDeactivateNotification, object: nil)
} else {
    NotificationCenter.default.addObserver(self, selector: #selector(taskFunc), name: UIApplication.willResignActiveNotification, object: nil)
}

[ 앱에 포그라운드로 돌아오는거 감지하기 ]
if #available(iOS 13.0, *) {
    NotificationCenter.default.addObserver(self, selector: #selector(taskFunc),
                                           name: UIScene.willEnterForegroundNotification, object: nil)
} else {
    NotificationCenter.default.addObserver(self, selector: #selector(taskFunc),
                                           name: UIApplication.willEnterForegroundNotification, object: nil)
}
[ 옵저버 죽이기 ]
/// 옵저버 없애기
override func viewWillDisappear(_ animated: Bool) {
    super.viewWillDisappear(animated)
    NotificationCenter.default.removeObserver(self)
}
