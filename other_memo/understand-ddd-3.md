# [わかる！ドメイン駆動設計 ～もちこちゃんの大冒険～【C91新刊】 - TechBooster - BOOTH](https://booth.pm/ja/items/392260)

4章です。

てか境界づけられたコンテキストってなんだよ。

## 境界づけられたコンテキスト

[境界づけられたコンテキスト 概念編 - ドメイン駆動設計用語解説 [DDD] - little hands&#39; lab](https://little-hands.hatenablog.com/entry/2017/11/28/bouded-context-concept)

要するに、AとBの場合違うからそれぞれ分けて考えろよってことでok?

[ドメイン駆動設計は何を解決しようとしているのか[DDD] - Qiita](https://qiita.com/little_hand_s/items/721afcbc555444663247#%E3%83%A2%E3%83%87%E3%83%AA%E3%83%B3%E3%82%B0%E3%81%8B%E3%82%89%E5%88%A9%E7%9B%8A%E3%82%92%E5%BE%97%E3%82%8B%E3%81%9F%E3%82%81%E3%81%AE%E3%82%A2%E3%83%97%E3%83%AD%E3%83%BC%E3%83%81)

ここの図がわかりやすかったかな。

以下用語とか調べた。

## Bounded Context

[境界づけられたコンテキスト 概念編 - ドメイン駆動設計用語解説 [DDD] - little hands&#39; lab](https://little-hands.hatenablog.com/entry/2017/11/28/bouded-context-concept)

[境界づけられたコンテキスト 実装編 - ドメイン駆動設計用語解説 - Qiita](https://qiita.com/little_hand_s/items/6e65ae050b873056c50c)

名前空間とかモジュールわけみたいなやつだ。

Hoge.Fugaみたなのあるやろ。

例えば、Foo.BarとHoge.Barがあっても別に重複しないわけだ。

でもうまく分けられてないとどっちのBarかわからんわけだよな。

そういうことか。そういうことでいいんだよな...?

んで、分割したこれらは別々のアプリとして考えた方がいいってことやよな。

いや、した方がいいってだけだが。

## ドメイン

本を読む前の私の認識: 特定の知識領域。

ドメインはサブドメインに分割できる。

## サブドメイン

本を読む前の私の認識: ドメインを分割したもの。

---

この先のコンテキストマップと連動する内容なので一緒にすればよかったね。
