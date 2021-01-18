# [ guard let self = self else { return } 정리 ]
https://jinsangjin.tistory.com/129

guard let self의 특징.
클로저가 종료될 때 까지 self(뷰컨)이 메모리에서 해제되지않음. ( 장점일수도 단점일수도. )

self?. 의 특징
self?구문 마다 self에 대한 nil을 체크함.
self?구문이 많으면 속도면에서 불리. ( 하지만 미미한 차이.. )

결론 :
클로저의 작업중, 뷰컨이 해제되면 안된다. -> guard let self
클로저의 작업중 뷰컨이 해제되도 상관없다. -> self?.
