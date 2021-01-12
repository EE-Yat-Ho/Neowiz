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

[ 영상 id로 유튜브 관련 정보 가져오기 ]
~~~
var apiKey = "AIzaSyBBuPq_YxJR9hDX4kbM8GaUYmusQfeC9qs"
var desiredChannelsArray = ["Apple", "Google", "Microsoft"]
var channelIndex = 0
var channelsDataArray: [[String:Any]] = []

func performGetRequest(targetURL: URL!, completion: @escaping (_ data: Data?, _ HTTPStatusCode: Int, _ error: Error?) -> Void) {
    var request = URLRequest(url: targetURL)
    request.httpMethod = "GET"

    let sessionConfiguration = URLSessionConfiguration.default

    let session = URLSession(configuration: sessionConfiguration)

    let task = session.dataTask(with: request) { data, response, error in
        DispatchQueue.main.sync {
            completion(data, (response as! HTTPURLResponse).statusCode, error )
        }
    }

    task.resume()
}

func getChannelDetails(useChannelIDParam: Bool) {
    var urlString: String!
    if !useChannelIDParam {
        urlString = "https://www.googleapis.com/youtube/v3/channels?part=contentDetails,snippet&forUsername=\(desiredChannelsArray[channelIndex])&key=\(apiKey)"
    }
    else {

    }

    let targetURL = URL(string: urlString)
    performGetRequest(targetURL: targetURL, completion: { (data, HTTPStatusCode, error) -> Void in
        if HTTPStatusCode == 200 && error == nil {
            // Convert the JSON data to a dictionary.
            guard let resultsDict = try? JSONSerialization.jsonObject(with: data!, options: []) as? [String: Any] else {
                return
            }

            // Get the first dictionary item from the returned items (usually there's just one item).
            guard let items = resultsDict["items"] as? [Any] else {
                return
            }

            guard let firstItemDict = items[0] as? [String: Any] else {
                return
            }

            // Get the snippet dictionary that contains the desired data.
            guard let snippetDict = firstItemDict["snippet"] as? [String: Any] else {
                return
            }

            // Create a new dictionary to store only the values we care about.
            var desiredValuesDict = [String: Any]()// = [String, Any]()
            desiredValuesDict["title"] = snippetDict["title"]
            desiredValuesDict["description"] = snippetDict["description"]
            desiredValuesDict["thumbnail"] = snippetDict["thumbnails"]

            // Save the channel's uploaded videos playlist ID.
            desiredValuesDict["playlistID"] = ((firstItemDict["contentDetails"] as! [String: Any])["relatedPlaylists"] as! [String: Any])["uploads"]

        }
    })
}
~~~
