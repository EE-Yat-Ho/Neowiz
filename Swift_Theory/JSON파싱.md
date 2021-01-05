# JSON파싱
1. 프로젝트에 JSON파일 넣기
2. 프로젝트 번들에 설정
[JSON 파일 읽어올 수 있게 Xcode 번들에 추가해야함]
https://stackoverflow.com/questions/41775563/bundle-main-pathforresourceoftypeindirectory-returns-nil

3. 
~~~
func loadJson(filename fileName: String) -> [CellData]? {
    if let url = Bundle.main.url(forResource: fileName, withExtension: "json") {
        do {
            let data = try Data(contentsOf: url)
            let decoder = JSONDecoder()
            let jsonData = try decoder.decode(CellDataes.self, from: data)
            return jsonData.data
        } catch {
            print("error:\(error)")
        }
    }
    return nil
}
~~~

4. JSON파일의 key값과 프로젝트의 변수명이 같아야함.
또한 구조체가 Decodable 을 채택해야함
구조체가 Decodable을 채택하려면 그 안에 있는 변수들도 Decodable 해야함
