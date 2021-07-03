# OS自作入門5日目

4日目は何も書くことがなかったので割愛します。

## 構造体

構造体については理解していたつもりだったが、この使い方は知らなかった。

まずnasmの方で以下のように記載していることが前提で、

```
CYLS	EQU		0x0ff0			; ブートセクタが設定する
LEDS	EQU		0x0ff1
VMODE	EQU		0x0ff2			; 色数に関する情報。何ビットカラーか？
SCRNX	EQU		0x0ff4			; 解像度のX
SCRNY	EQU		0x0ff6			; 解像度のY
VRAM	EQU		0x0ff8			; グラフィックバッファの開始番地
```

C側では以下のようにCYLSのアドレスで構造体を作れるらしい。

```
struct BOOTINFO *binfo = (struct BOOTINFO *) 0x0ff0;
```

アセンブラについて全然理解してない気がするので二周ぐらいしてみてもいいかもしれない。

## GDT

global (segment) descriptor tableの略。

よくわからんかったので[ここ](https://qiita.com/machine_engineer/items/90f0d085c1fef0a73b84)をみて補完した。

>側にGDT、右側にメモリ(memory)と書かれてありますね。この図を本に例えれば分かりやすいでしょう。左がわのGDTは本を読む際の目次だと考えればいいでしょう

なるほど。

## IDT

また[ここ](https://qiita.com/machine_engineer/items/90f0d085c1fef0a73b84)をみて補完した。の内容を抜粋するよ。

>簡単に言えば外部装置との繋がりです(正確ではないのですが、最初はそう考えても構わないでしょう。詳しくはグーグルで割り込みと調べれば出てきます。)。

わかったけどわからない。

ここで、もう一度本に戻って本文を見てみると、割り込み表みたいなものだという記載があった。

割り込み番号1が発生したらx関数を呼び出せといったような表らしい。

## 参考

[GDT、IDTを軽く説明（メモ）](https://qiita.com/machine_engineer/items/90f0d085c1fef0a73b84)
