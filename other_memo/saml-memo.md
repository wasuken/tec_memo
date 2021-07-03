# SAML

SAMLってたまに見るけどどんな認証でどこでつかわれるんだろうと思ったので少し調べた。

XML系っぽい名前だとは思ってたが、やはりXMLだった。

また、利用用途としては、主にシングルサインオンやID連携で利用されているらしい。

なるほど。OAuthと似たような役割なのだろうか。

どうやらOAuthは認可プロトコルで、SAMLは認証プロトコルらしい。

後、SAMLは複雑な権限処理も行えるらしい。けどOAuthもTwitter見た限りだえど

それなりに権限管理できてたような気がするがもっと複雑なことができるのだろうか。

それはそれとして、認可と認証の違いがよくわからんのでもっと調べてみたが、

どうやら認証とは本人確認までした上で、本人かどうかを確認することで、

認可は特定の権限が許可されてるかどうからしい。

# リンク

[OAuth vs SAML vs OpenID Connect vs SSO それぞれの違い。](https://baasinfo.net/?p=4418)

[Security Assertion Markup Language - wikipedia](https://ja.wikipedia.org/wiki/Security_Assertion_Markup_Language)

[オッス！オラ認証周りをまとめてみた](http://mnakajima18.hatenablog.com/entry/2016/05/04/205713)

[「認証と認可」について調べたので、違いをざっくり整理した](https://qiita.com/kaysquare1231/items/c4e4736f2a924b03777b)
