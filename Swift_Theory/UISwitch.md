[ UISwitch ]
온 오프 모션 개부드럽네 와..
알아보자
~~~
// 자동 로그인 스위치
private let autoLoginSwitch: UISwitch = UISwitch().then {
    $0.onTintColor = Resource.Color.bgYellow02
    $0.addTarget(self, action: #selector(autoLoginClick(sender:)), for: .valueChanged)
}
@objc func autoLoginClick(sender: UISwitch) {
    AccountManager.shared.setAutoLoginState(bool: sender.isOn)
    sender.thumbTintColor = sender.isOn ? Resource.Color.orange01 : nil
}
~~~
개꿀
잘만들어놔줘서 고맙습니다 애플님들 ^_^7
