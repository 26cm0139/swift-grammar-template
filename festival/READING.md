# 読解ノート：自分のアプリのコード3箇所

> **氏名：** リアンき
> **AI利用レベル：** 3（質問のみ。説明は自分の言葉で書く）
> **最終更新：** 2026-10-16

生成AIに書いてもらったコードでも、自分で書いたコードでもかまいません。自分のアプリの中から3箇所を選んで、次の3つの問いに答えてください。分からないところは、生成AIに「この行は何をしていますか」「この行を消すとどうなりますか」と聞いてかまいません。ただし、書くのは自分の言葉です。

> 💡 担任の先生の指示で、項目が増えることがあります。

---

## 箇所1：現在地を取得する処理

```swift
// 該当部分のコードを抜粋して貼る（5〜15行くらい）
```
func locationManager(
    _ manager: CLLocationManager,
    didUpdateLocations locations: [CLLocation]
) {
    if let newLocation = locations.last {
        location = newLocation
        manager.stopUpdatingLocation()
    }
}


**何をしているか：**
ユーザーの現在地を取得するための処理です
**なぜこう書くのか：**

if let を使うことで、位置情報があるかどうかを安全に確認できます。

**もしこう書かなかったら：**

if let を使わないと、位置情報がない場合の処理に注意する必要があります。
---

## 箇所2：現在地を取得した後の店舗検索

```swift
// コードを貼る
```
.onChange(of: locationManager.location) { oldValue, newValue in
    if let newLocation = newValue {
        if hasSearched == false {
            hasSearched = true
            searchRestaurants(userLocation: newLocation.coordinate)
        }
    }
}
**何をしているか：**
ユーザーの現在地を取得した後、近くのお店を検索する処理です
**なぜこう書くのか：**
onChange を使うことで、位置情報が変わったタイミングで検索できます
**もしこう書かなかったら：**
この処理がないと、現在地を取得しても、お店の検索が自動で始まりません。
---

## 箇所3：結果に合わせて効果音を再生する処理

```swift
// コードを貼る
```
func playConfirm(rare: Bool) {
    guard Feedback.soundEnabled else { return }
    if let player = rare ? rarePlayer : confirmPlayer {
        player.currentTime = 0
        player.play()
    } else {
        AudioServicesPlaySystemSound(rare ? 1025 : 1057)
    }
}
**何をしているか：**
普通の結果とレアな結果で違う音を再生します。また、音の設定がオフの場合は、音を出さないようにしています。
**なぜこう書くのか：**
レアな料理が出たときの特別な感じを出したかったからです
**もしこう書かなかったら：**
アプリの楽しさが減ると思います
---

## 自分ではまだ説明できない箇所（正直に）

（アプリの中で「動いているけれど何をしているか分からない」ところを書く。ここに書いたものは、後期の文法の授業で分かるようになります。）
private func sweepAway() {
        guard !sweep else { return }
        Feedback.impact(.soft)
        withAnimation(.easeIn(duration: 0.32)) {
            sweep = true
        }
        DispatchQueue.main.asyncAfter(deadline: .now() + 0.3) {
            onDismiss()
        }
    }
}
