[ Rx <-> combine 비교글 ]
https://medium.com/gett-engineering/rxswift-to-apples-combine-cheat-sheet-e9ce32b14c5b
옵저버 = 서브스크라이벌 ㅇㅈ
CurrentValueSubject = BehaviorSubject ( 상태값 존재 )
DisposeBag = A collection of AnyCancellables .. tq : Call anyCancellable.stroe(in: collection), where collection can be an array, a set, or any other RangeReplaceableCollection
옵저버블 = 퍼블리셔
PassthroughSubject = PublishSubjevt
Single = Future
asObservable() = eraseToAnyPubliser()
bind(to:) = assign(to:on:)
do = handleEvents
distinctUntilChanged = removeDuplicates
elementAt = output(at:)
just = Just
map = map
observeOn = receive(on:)
subscribe = sink


[ 혼자 파악한거 ] (역시 삽질이 답이지)
* subject끼리 이어주기 = subscribe(subject)
* subject에 클로저 이어주기 = sink
* subject에 프로퍼티값 이어주기 = assign
* subject에 이벤트 푸시 = send
