# 検索エンジン自作入門～手を動かしながら見渡す検索の舞台裏

[検索エンジン自作入門～手を動かしながら見渡す検索の舞台裏 | 山田浩之, 末永匡 | 工学 | Kindleストア | Amazon](https://www.amazon.co.jp/dp/B00NUZ32MU/ref=dp-kindle-redirect?_encoding=UTF8&btkr=1)

やっていき。

## 五章

### 圧縮

#### 圧縮方法

##### unary

整数値x(>0)をx-1個の"1"ビットと、1個の"0"ビットで表現する方法。

##### gamma, delta

gammaはx(>0)を2^e+d(e=log2x, 0 <= d < 2^e)に分解し、e+1をunaryで、dをeビットのバイナリ符号で表現する方法。

deltaはgammaにおいて、unaryで符号化する部分をgamma符号で置き換える。

##### variable-byte, byte-aligned

整数を複数のバイト列で表現する符号化方法。

この程度の圧縮で変わるもんなのか...?

##### Golomb

[ゴロム符号 - Wikipedia](https://ja.wikipedia.org/wiki/%E3%82%B4%E3%83%AD%E3%83%A0%E7%AC%A6%E5%8F%B7)
