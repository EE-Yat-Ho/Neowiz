[ 키체인 ]
https://kor45cw.tistory.com/285
유저디폴트는 base64 인코딩을 하지만, 높은 수준의 보안이 아님.
민감한 정보는 키체인을 이용하여 저장하기

SecKeychain = 디비
SecKeychainItem = Item

iOS는 단일 키체인 ( 자신 and 자신이 속한 그룹과 공유하는 item만 접근 )
macOS는 여러개의 키체인 ( 키체인 접근 알지? 그게 폰에도 있단겨 )

앱이 지워져도 유지 ㄷ;ㄷ;

SecKeychain 라는 디비가 있으며
이 디비에는 SecKeychainItem을 넣는다.
Item에는 애플이 미리 지정한 각종 어트리뷰트들 kSecAttr이 있으며
kSecAttr 중에 어떤 것들을 키(키체인 항목), 어떤 것들을 밸류로 사용할지 프로프래머가 지정한다.

Keychain 관련 쿼리 키 값들
let kSecClassValue                  = NSString(format: kSecClass)
let kSecAttrAccountValue            = NSString(format: kSecAttrAccount)
let kSecValueDataValue              = NSString(format: kSecValueData)
let kSecAttrGenericValue            = NSString(format: kSecAttrGeneric)
let kSecAttrServiceValue            = NSString(format: kSecAttrService)
let kSecAttrAccessValue             = NSString(format: kSecAttrAccessible)
let kSecMatchLimitValue             = NSString(format: kSecMatchLimit)
let kSecReturnDataValue             = NSString(format: kSecReturnData)
let kSecMatchLimitOneValue          = NSString(format: kSecMatchLimitOne)
let kSecAttrAccessGroupValue        = NSString(format: kSecAttrAccessGroup)
let kSecClassGenericPasswordValue   = NSString(format: kSecClassGenericPassword)
~~~
private let kSecAttrServiceStr: String = "kkPoint"
private let kSecAttrAccountStr: String = "user"

/// SecItemAdd함수를 사용해, 키체인 아이템 추가. 성공시 true
func saveUserItem(_ user: KKPointUser) -> Bool {
    // 토큰셋을 JSON 인코딩하여 data로 가공
    guard let data = try? JSONEncoder().encode(user) else { return false }
    // data를 저장하기 위한 쿼리 (
    let query: [CFString: Any] = [kSecClass: kSecClassGenericPassword, // 키체인 항목을 어떤 방식으로 만드느냐.
                                  //kSecClassGenericPassword는 kSecAttrService와 kSecAttrAccount의 조합을 사용.
                                  kSecAttrService: kSecAttrServiceStr, // 키체인 항목에 넣을 kSecAttrService의 값
                                  kSecAttrAccount: kSecAttrAccountStr, // 키체인 항목에 넣을 kSecAttrAccount의 값
                                  kSecAttrGeneric: data] // Generic이라는 attr를 밸류로 사용한다.
    deleteUserItem() // 이미 있는 거 삭제 (이미 있을 때 Create하면 실패함) SecItemDelete만 하니까 안됨
    return SecItemAdd(query as CFDictionary, nil) == errSecSuccess
 }

/// SecItemCopyMatching함수를 사용해, 키체인 아이템 로드. 성공시 읽은 tokenSet
func loadUserItem() -> KKPointUser? {
    let query: [CFString: Any] = [kSecClass: kSecClassGenericPassword,
                                kSecAttrService: kSecAttrServiceStr,
                                kSecAttrAccount: kSecAttrAccountStr,
                                kSecMatchLimit: kSecMatchLimitOne,
                                kSecReturnAttributes: true,
                                kSecReturnData: true]

    var item: CFTypeRef?
    if SecItemCopyMatching(query as CFDictionary, &item) != errSecSuccess { return nil }

    guard let existingItem = item as? [CFString: Any],
          let data = existingItem[kSecAttrGeneric] as? Data,
          let user = try? JSONDecoder().decode(KKPointUser.self, from: data) else { return nil }

    return user
}

/// SecItemDelete함수를 사용해, 키체인 아이템 삭제. 성공시 true
func deleteUserItem() -> Bool {
  let query: [CFString: Any] = [kSecClass: kSecClassGenericPassword,
                                kSecAttrService: kSecAttrServiceStr,
                                kSecAttrAccount: kSecAttrAccountStr]

  return SecItemDelete(query as CFDictionary) == errSecSuccess
}

/// SecItemUpdate함수를 사용해, 키체인 아이템 수정. 성공시 true
//    func updateTokenItem(_ user: TokenSet) -> Bool {
//      guard let data = try? JSONEncoder().encode(user) else { return false }
//
//      let query: [CFString: Any] = [kSecClass: kSecClassGenericPassword,
//                                    kSecAttrService: kSecAttrServiceStr,
//                                    kSecAttrAccount: kSecAttrAccountStr]
//      let attributes: [CFString: Any] = [kSecAttrAccount: "tokenSet",
//                                         kSecAttrGeneric: data]
//
//      return SecItemUpdate(query as CFDictionary, attributes as CFDictionary) == errSecSuccess
//    }
~~~
