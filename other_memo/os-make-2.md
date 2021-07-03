# どうしたものか

前回の記事で見つけたリンクだが、どこまで流用すれば一番学習効率が良いのかわからない。

アセンブラ学んだ。

* DB命令

data byteの略で、ファイルの内容を１Byteだけ直接書く命令。

* RESB命令

reserve byteの略で、１０Byte予約するという意味らしい。Cでいうmallocなのかな。わからん。

[OS自作入門](https://qiita.com/tatsumack/items/491e47c1a7f0d48fc762)ではnaskというツールを
利用しており、

naskでは0x00で埋めてくれるみたいで、そのために利用しているらしい。

* DW命令

data wordの略wordという直訳で、２Byteある。

* DD命令

data double-wordの略。４Byteある。

* RESB 0x1fe-$

なんだこれ。この行が先頭から何Byte目かを教えてくれる変数らしい。
